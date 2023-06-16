# Hướng Dẫn Dùng Git

Tổng quan về git:  

Git dùng để quản lí mã nguồn, nó lưu trữ versions của mã code thông qua những cái log mà chúng ta đã commit và giúp dễ dàng revert khi có các code lỗi.  
![alt text](./img/git.png)  

Dùng `git init` để tạo khởi tạo git, lần commit đầu tiên mình gọi c0 (như hình trên) Git sẽ tạo một commit đầu tiên trong lịch sử của kho lưu trữ đó. Commit này thường được gọi là "commit khởi nguyên" hoặc "commit đầu tiên". Trong Git, commit đầu tiên này thể hiện trạng thái ban đầu của dự án và chứa thông tin về thư mục và tệp tin hiện có. 

Mỗi lần commit, git sẽ tạo ra một node. Các node liên kết với nhau bằng tham chiếu (reference). Các bạn cứ hiểu một node sẽ chứa các thông tin về sự thay đổi của dự án. Khi bạn tạo commit c1, git sẽ tự động ghi nhận thông tin về commit cha (c0) và lưu trữ tham chiếu đến commit cha (c0). Điều này cho phép Git theo dõi sự lịch sử của các commit và tạo ra một chuỗi các commit được liên kết với nhau theo trình tự thời gian. Thông qua các tham chiếu commit cha, Git cho phép bạn đi ngược lại trong lịch sử commit, từ đó khôi phục các phiên bản trước đó của dự án.  

Một số lệnh cơ bản thường dùng bao gồm: `git init`, `git clone`, `git add`, `git commit`, `git push`, `git pull`, và `git merge`. 

### Các commands thường hay sử dụng

| Commands | Giải thích |
| --- | --- |
| `git init` | Lệnh này được sử dụng để khởi tạo một kho chứa Git mới trong thư mục hiện tại. Khi chạy `git init`, Git sẽ tạo ra một kho chứa trống để bạn có thể bắt đầu quản lý phiên bản mã nguồn. |
| `git clone` | Lệnh này được sử dụng để sao chép (clone) một kho chứa Git từ một URL xa vào máy tính của bạn. Khi chạy `git clone`, Git sẽ tải về toàn bộ lịch sử và mã nguồn từ kho chứa từ xa và tạo ra một bản sao hoàn chỉnh trên máy tính của bạn. |
| `git add [file path]` | Lệnh này được sử dụng để thêm một hoặc nhiều file vào vùng staging (vùng chuẩn bị) để chuẩn bị cho commit. Bằng cách chạy `git add`, bạn cho phép Git theo dõi các thay đổi trong file đã chỉ định. |
| `git commit -m "[message]"` | Lệnh này tạo một commit mới với các thay đổi đã được thêm vào vùng staging. Bằng cách chạy `git commit`, bạn ghi lại trạng thái hiện tại của mã nguồn và gắn kèm một thông điệp mô tả cho commit đó. |
| `git pull` | Lệnh này được sử dụng để lấy (pull) các commit mới nhất từ một kho chứa từ xa và tích hợp (merge) chúng vào nhánh hiện tại. Khi chạy `git pull`, Git tải về các commit mới nhất và tự động thực hiện quá trình merge để tích hợp nội dung mới vào dự án của bạn. |
| `git merge [branch]` | Lệnh này được sử dụng để gộp các thay đổi từ một nhánh khác vào nhánh hiện tại. Khi chạy git merge, Git sẽ kết hợp (merge) các thay đổi từ nhánh được chỉ định vào nhánh hiện tại của bạn. |
| `git push` | Lệnh này được sử dụng để đẩy (push) các commit đã tạo lên một kho chứa từ xa. Khi chạy `git push`, Git gửi các commit mới nhất từ nhánh hiện tại của bạn lên kho chứa từ xa để chia sẻ với người khác. |
| `git rebase` | Lệnh trong Git được sử dụng để tái cấu trúc lịch sử commit trong một nhánh. Khi sử dụng `git rebase`, các commit trong nhánh hiện tại sẽ được chuyển đổi thành các commit mới dựa trên một commit gốc hoặc một nhánh khác. |

**Thay đổi nhỏ:** 
>Trước phiên bản Git 2.23, để chuyển đổi (switch) giữa các nhánh hoặc commit trong Git, người ta dùng thường sử dụng lệnh `git checkout`. Tuy nhiên, từ phiên bản 2.23 trở đi, Git đã giới thiệu lệnh `git switch` nhằm mục đích rõ ràng hơn và an toàn hơn cho việc chuyển đổi giữa các nhánh hoặc commit. Tên lệnh: `git switch` nghe cái tên thôi cũng đã phản ánh rõ ràng hơn về mục đích sử dụng, trong khi git checkout có nhiều mục đích hơn (như chuyển đổi nhánh, chuyển đổi commit, tạo nhánh mới, vv.), dễ gây nhầm lẫn hơn trong việc sử dụng. Cuối cùng là Master hãy chuyển thành Main.  

## Git Flow  
![alt text](./img/gitflow-hotfix-branch-diagram.jpg)  
> Tuyệt đối! các bạn không nên sửa đổi file trên nhánh Main(Master). Muốn làm feature mới thì hãy `git checkout` ra một nhánh mới rồi hẳn làm. Sau khi hoàn thành feature đó hãy merge vào nhánh Main.  
 
Để quản lí một dự án hiệu quả PM sẽ tạo ra 5 nhánh như hình trên, mình sẽ thay thế nhánh `master` thành `main` để hợp với thuần phong mỹ tục hiện nay &#x1F600;.  

Trong Git Flow, nhánh `main` thường được sử dụng làm nhánh chính để triển khai (deploy) sản phẩm (product) hoặc phiên bản ổn định của dự án. Nhánh main thường chứa mã nguồn ổn định và được coi là phiên bản chính thức của sản phẩm.  

Khi sử dụng Git Flow, công việc phát triển mới thường được thực hiện trên các nhánh khác như `develop` hoặc các nhánh tính năng (feature branches). Khi một tính năng hoặc một chuỗi các tính năng hoàn thành, chúng được merge vào nhánh `develop` để kiểm tra tích hợp và kiểm tra chất lượng để chuẩn bị merge vào nhánh `release`.  

Sau khi hoàn thành việc phát triển từ nhánh `develop` tiến hành merge vào nhánh `release`, ở nhánh này bạn thực hiện các công việc cuối cùng như kiểm tra, kiểm tra tích hợp, kiểm tra hệ thống và các chỉnh sửa cuối cùng trước khi đưa sản phẩm. Sau khi tiến hành kiểm tra kỹ lưỡng, merge nhánh `release` vào nhánh `main` và `develop`. Merge vào nhánh `develop` để lữu trữ version code mới nhất của sản phẩm chuẩn bị cho việc phát triển version tiếp theo của sản phẩm (nếu có).  

Sau đó, khi sản phẩm chuẩn bị để triển khai, nhánh `release` sẽ được merge vào nhánh `main`. Việc này đồng nghĩa với việc những thay đổi mới nhất trên `release` được đưa vào nhánh main và sẵn sàng để triển khai lên môi trường sản phẩm. Quy trình này giúp tách riêng phần phát triển và tích hợp từ phần triển khai và triển khai sản phẩm. Nhánh `main` trong Git Flow thường được coi là nhánh ổn định và an toàn để xây dựng sản phẩm và triển khai cho người dùng cuối.  

Sản phẩm đang triển khai cho người dùng cuối sử dụng chẳng may phát sinh ra lỗi (bug), ta sẽ tạo một nhánh `hotfix` từ nhánh `main` để xử lý và vá các lỗi gấp cần phải sửa ngay trên phiên bản sản phẩm đang được triển khai. Nhánh `hotfix` cho phép bạn tách riêng công việc sửa lỗi khẩn cấp và triển khai các thay đổi liên quan mà không ảnh hưởng đến quy trình phát triển đang diễn ra trên nhánh `develop`.  

Khi các sửa đổi đã được hoàn thành và kiểm tra, merge nhánh `hotfix` vào cả nhánh `main` và `develop`. Merge vào nhánh `main` đảm bảo rằng các thay đổi sửa lỗi được áp dụng ngay vào phiên bản sản phẩm chính đang được triển khai. Merge vào nhánh `develop` đảm bảo rằng các sửa đổi cũng phải được tích hợp vào quy trình phát triển sản phẩm đang được triển khai trên nhánh `develop` để lần release tiếp theo không bị lỗi.



[Luyện Git](https://learngitbranching.js.org/)