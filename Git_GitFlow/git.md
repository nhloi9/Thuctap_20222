## GIT, GIT FLOW

## 1.Tổng quan

### 1.1. Version Control System

Hệ thống quản lý phiên bản

- VCS là một hệ thống giúp lưu trữ các thay đổi của tập hợp các tập tin theo thời gian.
- VCS giúp:
  - Khôi phục lại phiên bản cũ của các file
  - Khôi phục lại phiên bản cũ của toàn bộ dự án
  - Xem lại các thay đổi đã được thực hiện theo thời gian
  - Xem người thực hiện thay đổi...

### 1.2. Local Version Control Systems (LVCSs)

Hệ thống quản lý phiên bản cục bộ

- Thực hiện copy các file sang một thư mục khác -> đơn giản nhưng dẽ gây lỗi, khó quản lý -> Khắc phục: dùng một database đơn giản lưu trữ tất cả sử thay đổi của các files qua các phiên bản.

  [![1567913881879](https://github.com/viethungbk/internship-report/raw/master/git/images/Local-VCS.png)](https://github.com/viethungbk/internship-report/blob/master/git/images/Local-VCS.png)

- Hệ thống quản lý phiên bản RSC (được sử dụng trên HĐH Mac OS X): lưu giữ các bản vá ~ sự thay đổi của các files ở các phiên bản -> có thể khôi phục các files bằng các gộp các bản vá với nhau.

### 1.3. Centralized Version Control Systems (CVCSs)

Hệ thống quản lý phiên bản tập trung

- LVCSs không giải quyết được vấn đề làm việc nhóm trong một hệ thống

  -> Cần CVCSs

- Gồm:

  - Máy chủ chứa tất cả các tập tin được versioned
  - Danh sách máy khách có quyền thay đổi các tập tin đó

  [![1567914656059](https://github.com/viethungbk/internship-report/raw/master/git/images/Central-VCS.png)](https://github.com/viethungbk/internship-report/blob/master/git/images/Central-VCS.png)

- Ưu điểm:

  - Có thể biết được công việc người khác làm trong dự án
  - Quản lý có thể quản lý người dùng, files theo ý muốn
  - Làm việc nhóm dễ dàng hơn so với LVCSs

- Nhược điểm:

  - Tập trung -> Máy chủ hỏng -> Mất toàn bộ dữ liệu, chỉ còn các phiên bản trên máy cục bộ

### 1.4. Distributed Version Control Systems (DVCSs)

Hệ thống quản lý phiên bản phân tán

- Gồm:

  - Máy chủ chứa các tập tin được versioned
  - Máy khách sao chép toàn bộ repository

  -> Khắc phục vấn đề của CVCSs: khi máy chủ ngừng hoạt động, máy khách có thể sao chép ngược về máy chủ đề khôi phục toàn bộ hệ thống

  [![1567915438524](https://github.com/viethungbk/internship-report/raw/master/git/images/Distributed-VCSs.png)](https://github.com/viethungbk/internship-report/blob/master/git/images/Distributed-VCSs.png)

### 1.5. A short history of Git

Sơ lược lịch sử của Git

- Trong thời gian bảo trì của nhân Linux (1991-2002), các thay đổi của phần mềm được truyền đi dưới dạng các bản vá và tập tin lưu trữ
- Năm 2002, dự án nhân Linux bắt đầu sử dụng DVCS độc quyền là BitKeeper
- Năm 2006, sự hợp tác giữa cộng đồng phát triển nhân Linux và công ty thương mại phát triển BitKeeper bị phá vỡ, và công cụ đó không được cung cấp miễn phí nữa.
- Điều này thúc đấy cộng đồng phát triển Linux (Linus Torvalds - người sáng lập ra Linux) phát triển công cụ của riêng họ dựa trên việc sử dung BitKeeper
- Mục tiêu chính của hệ thống:
  - Nhanh
  - Thiết kế đơn giản
  - Hỗ trợ tốt cho phát triển phi tuyển tính (non-linear development)
  - Phân tán toàn diện
  - Có khả năng xử lý các dự án lớn hiệu quả

### 1.6. What is Git ?

#### 1.6.1. GIt vs. other VCS

Git với các VCS khác

- Các VCS khác:

  - Lưu trữ thông tin dưới dạng danh sách các tập tin được thay đổi: coi thông tin được lưu trữ như là một tập tin và các thay đổi được thực hiện trên mỗi tập tin theo thời gian

    [![1567922892053](https://github.com/viethungbk/internship-report/raw/master/git/images/Other-VCS.png)](https://github.com/viethungbk/internship-report/blob/master/git/images/Other-VCS.png)

- Git:

  - Coi dữ liệu như một tập các snapshot của hệ thống tập tin nhỏ, Mỗi lần commit thì Git chụp một bức ảnh ghi lại nội dung của tất cả cá tập tin tại một thời điểm đó và tạo một tham chiếu tới snapshot đó.

  - Tập tin không có thay đổi sẽ không lưu trữ lại mà chỉ tạo một liên kết tới tập tin gốc đã tồn tại trước đó.

    [![1567923157048](https://github.com/viethungbk/internship-report/raw/master/git/images/Git.png)](https://github.com/viethungbk/internship-report/blob/master/git/images/Git.png)

#### 1.6.2. The three States

Ba trạng thái

- Mỗi tập tin được quản lý dữ trên 3 trạng thái:

  - Commited: dữ liệu được lưu trữ an toàn trong database
  - Modified: đã thay đổi tập tin nhưng chưa commit và database
  - Staged: đã đánh dấu sẽ commit phiên bản hiện tại của một tập tin đã chỉnh sửa trong lần commit sắp tới

- Ba phần của một dự án sử dụng Git:

  - Git directory: chưa metadata và database cho dự án, được sao lưu về khi clone một repository từ máy tính khác
  - Working directory: là bản sao một phiên bản của dự án. Tập tin này được pulled từ database, nén lại trong Git directory và lưu trên ổ cứng để sử dụng và chỉnh sửa.
  - Staging area: là một tập tin được chứa trong Git directory, chứa thông tin về những gì được commit trong lần commit sắp tới

- Workflow cơ bản của Git:

  1.  Thay đổi các file trong Working directory
  2.  Tổ chức các tập tin, tạo mới snapshot bằng cách stage các thay đổi vào Staging area
  3.  Commit, lưu các tập tin trong Staging area vào Git directory

  [![1567924535800](https://github.com/viethungbk/internship-report/raw/master/git/images/Main-sections-Git-project.png)](https://github.com/viethungbk/internship-report/blob/master/git/images/Main-sections-Git-project.png)

### 1.7. The Command Line

### 1.8. Installing Git

### 1.9. First time Git setup

- Tên tài khoản và email:

  ```
  git config --global user.name "name"

  ```

  ```
  git config --global user.email email@example.com

  ```

- Trình soạn thảo:

  ```
  git config --global core.editor vim

  ```

- Công cụ so sánh thay đổi:

  ```
  git config --global merge.tool vimdiff

  ```

## 2: Git Basics

### 2.1. Getting a Git Repository

Tạo một kho chứa Git Có hai cách chính:

- Tạo một kho chứa từ thư mục cũ:

  ```
  git init

  ```

- Sao chép một kho chứa đã tồn tại:

  ```
  git clone [url] [folder_name]

  ```

### 2.2. Recording changes to the repository

Lưu thay đổi vào kho chứa

- Trạng thái của file:

  - `tracked`: đã có mặt trong snapshot trước, chúng có thể là `unmodified`, `modified`, hoặc `staged`
  - `untracked`: file trong working directory mà không cho snapshot ở lần commit trước hoặc không ở trong staging area.

  [![1567937275187](https://github.com/viethungbk/internship-report/raw/master/git/images/File-status-lifecycle.png)](https://github.com/viethungbk/internship-report/blob/master/git/images/File-status-lifecycle.png)

- Kiểm tra trạng thái của file:

  ```
  git status

  ```

- Theo dõi các file mới:

  ```
  git add [file_name]

  ```

- Bỏ qua các file: Tạo một tập tin mới có tên `.gitignore` và liệt kê các patterns muốn bỏ qua.

- Commit thay đổi:

  ```
  git commit -m "[message]"

  ```

### 2.3. Viewing the commit history

Xem lịch sử commit

```
git log

```

### 2.4. Undoing things

#### 2.4.1. Undo the latest commit

Thay đổi commit cuối cùng:

- Khi commit chưa như ý muốn và muốn thực hiện commit lại commit cuối cùng:

  ```
  [do something: add file,...]
  git commit --amend

  ```

#### 2.4.2. Unstaging a staged file

Loại bỏ tập tin đã staged (đã đưa vào staging area)

```
git reset HEAD [file_name]

```

#### 2.4.3 Unmodifying a modified file

Phục hồi tập tin đã thay đổi

```
git checkout -- [file_name]

```

### 2.5. Working with remotes

#### 2.5.1. Showing your remotes

- Để liệt kê tên ngắn gọn của mỗi máy chủ từ xa đã chỉ định:

```
git remote

```

- Nếu sao chép từ một repository sẽ thấy  `bản gốc` (origin)
- Sử dụng tham số `-v` để hiển thị địa chỉ mà Git đã lưu tên rút gọn đó:

```
git remote -v

```

---

## 3.Git Flow

### 3.1 Khái niệm

Git Flow được [Vincent Driessen](http://nvie.com/posts/a-successful-git-branching-model/) đưa ra nhằm cải thiện quá trình làm việc cùng Git. Thực chất, đấy là cách chia nhánh và merge nhánh vào khi hoàn thành một tập hợp tính năng hoặc fix.

Git Flow đưa ra các quy ước để triển khai công việc. Nó được tổng kết qua quá trình làm việc thực tiễn của nhiều team trên thế giới. Mục đích là các nhóm công việc triển khai song song nhưng không ảnh hưởng tới nhau. Các  môi trường development, staging và production tách biệt giúp quá trình kiểm thử (QA), feedback và xử lý các issue được gọn gàng và thống nhất hơn.

![](https://static.wixstatic.com/media/20d819_4dc550871b9c4c4d8936f0a766536946~mv2.png/v1/fill/w_1175,h_440,al_c,q_90,usm_0.66_1.00_0.01,enc_auto/20d819_4dc550871b9c4c4d8936f0a766536946~mv2.png)

### 3.2 Các branch chính

---

- master: là branch tồn tại xuyên suốt quá vòng đời của phần mềm được tạo mặc định trong Git khi ta tạo repository.

- develop: là nơi các develop phát triển chính branch luôn tồn tại song song với master

- feature: là nhánh được tách từ develop nhằm mục đích xây dựng các tính năng riêng mà không phụ thuộc vào nhau

- release: là nhánh tách từ develop để kiểm tra và fix bug chuẩn bị cho việc ra mắt sản phẩm

- hotfix: là nhánh tách từ master để fix gấp những bug còn tồn đọng mà trên release chưa xử lý hết

#### 3.2.1\. Master

![](https://static.wixstatic.com/media/20d819_11ecdfc37c22405bbf8cc0c472711651~mv2.png/v1/fill/w_450,h_678,al_c,q_85,usm_0.66_1.00_0.01,enc_auto/20d819_11ecdfc37c22405bbf8cc0c472711651~mv2.png)

- Đây là branch chính của cả dự án chỉ có thể merge vào từ branch release chứ không được code trực tiếp trên branch này. Sản phẩm được đưa lên production sẽ được lấy ở đây nên code được merge vào master phải được quản lý và xử lý cẩn thận nhất có thể.

### 3.2.2\. Develop

- Branch develop là branch trung tâm cho việc phát triển.

- Mỗi khi có tính năng mới cần xây dựng thì branch feature sẽ được tách từ branch develop để phát triển

- Mỗi khi chuẩn bị release phiên bản mới thì branch release sẽ được tách từ branch develop để test

#### 3.2.3\. Feature

![](https://static.wixstatic.com/media/20d819_58a1e2c61def41d09b78e4bee7badeca~mv2.png/v1/fill/w_319,h_857,al_c,lg_1,q_85,enc_auto/20d819_58a1e2c61def41d09b78e4bee7badeca~mv2.png)

- Các branch feature được sử dụng để phát triển các tính năng mới cho bản release sắp tới hoặc trong tương lai xa. Branch feature sẽ tồn tại miễn là tính năng này đang được phát triển, nhưng cuối cùng sẽ được hợp nhất trở lại develop(khi thêm tính năng mới vào bản release sắp tới) hoặc bị loại bỏ (trong trường hợp thử nghiệm đáng thất vọng).

- Các nhánh tính năng thường tồn tại trong repo của dev, không phải trong origin.

- Ngoài các tính năng chính thì còn có thể tách thành cách tính năng nhỏ hơn để thuận tiện cho việc phát triển tùy vào cấu trúc cũng như độ phức tạp của dự án

#### 3.2.4\. Release

- Branch release là branch dùng để release sản phẩm như đúng tên gọi của nó. Khi khách hàng cần release một số tính năng thì một branch sẽ được tách từ branch develop ra với tên theo cấu trúc "release/v.1.0.1" . Sau đó sẽ test và fix bug trên branch release, khi xong sẽ merge vào branch master để đẩy sản phẩm lên và merge vào branch develop để tránh gặp lại các bug đã được test và fix.

#### 3.2.5\. Hotfix

![](https://static.wixstatic.com/media/20d819_0feed90969d447d9927b0c56eb6fbe35~mv2.png/v1/fill/w_450,h_606,al_c,q_85,usm_0.66_1.00_0.01,enc_auto/20d819_0feed90969d447d9927b0c56eb6fbe35~mv2.png)

Có 2 trường hợp thường xảy ra:

- Có những bug mà trong quá trình sử dụng thực tế người dùng phát hiện ra mà QA không test được

- Đôi lúc vì một số lý do khách hàng muốn ra mắt ngay tính năng mới đang phát triển trên develop. Và tất nhiên khi đẩy trực tiếp như thế sẽ xuất hiện một lỗi nghiêm trọng trong phiên bản release.

-> Vì code trên master phải là code release được nên nếu có bug nó phải được ưu tiên sửa chữa ngay. Từ master branch hotfix sẽ được tạo và xử lý khi xong sẽ lại được merge vào master và develop.
