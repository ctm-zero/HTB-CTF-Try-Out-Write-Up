# **An unusual sighting**
>As the preparations come to an end, and The Fray draws near each day, our newly established team has started work on refactoring the new CMS application for the competition. However, after some time we noticed that a lot of our work mysteriously has been disappearing! We managed to extract the SSH Logs and the Bash History from our dev server in question. The faction that manages to uncover the perpetrator will have a massive bonus come competition!

Tải scenario files và giải nén nó, ta có được hai tệp forensics_an_unusual_sighting và __MACOSX.
Bỏ qua __MACOSX và vào tệp còn lại, ta thấy được hai file quan trọng: bash_history và sshd.log
Bắt đầu docker có câu hỏi đầu tiên:
> What is the IP Address and Port of the SSH Server (IP:PORT)

Dễ dàng thấy được phần lớn các kết nối trong sshd.log là hướng vào **100.107.36.130:2221**
<img width="825" height="275" alt="Screenshot from 2025-11-13 23-03-39" src="https://github.com/user-attachments/assets/d8753ec1-3eee-4670-b3cb-e9ddfc0f5355" />

<img width="478" height="69" alt="image" src="https://github.com/user-attachments/assets/37134618-dc08-462b-91ce-eb01e71323ee" />

>What time is the first successful Login

Cũng dễ dàng thấy trong sshd.log, Login đầu tiên thành công là vào **2024-02-13 11:29:50**
<img width="822" height="78" alt="image" src="https://github.com/user-attachments/assets/d0d2d029-5077-4cca-a723-13eb7aa74972" />

>What is the time of the unusual Login

Bắt đầu vào vấn đề chính của challenge. Nhìn vào sshd.log, nhìn lướt qua thấy phần lớn các connection là đến từ
softdev. Chỉ có 3 lần duy nhất connect tới root
+ Lần thất bại từ 100.72.1.95:47721 vào lúc 2024-01-28 15:24:24
+ Lần thành công từ 100.81.51.199:63172 vào lúc 2024-02-13 11:29:50
+ Lần thành công từ 2.67.182.119:60071 vào lúc 2024-02-19 04:00:14

Bỏ qua lần kết nối thất bại, ta chỉ quan tâm tới 2 lần thành công. Đối chiếu thời gian với bash_history.txt. Ta thấy:
+ Lần thành công thứ nhất, root được sử dụng để thiết lập hệ thống và tạo user softdev
<img width="960" height="255" alt="image" src="https://github.com/user-attachments/assets/587de8af-0489-4da6-a1ae-f3cfaa0b61bc" />
Không có gì đáng nghi cả!
+ Lần thành công thứ hai, root được sử dụng khá lạ
<img width="931" height="152" alt="image" src="https://github.com/user-attachments/assets/a8e0d8ff-c66d-4259-8133-269783a6c7f4" />

Đây chính là đối tượng cần tìm

<img width="312" height="67" alt="image" src="https://github.com/user-attachments/assets/44606b61-8d78-4862-a5cc-a947cac734d7" />

Biết được đối tượng, dễ dàng trả lời được 3 câu hỏi cuối cùng và lấy được flag
<img width="540" height="224" alt="image" src="https://github.com/user-attachments/assets/69d0a684-12cd-44ef-9805-04979d0f2c5f" />
