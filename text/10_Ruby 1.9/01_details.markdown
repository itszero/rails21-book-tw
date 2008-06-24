## 詳細資訊 (Details)

Rails的修改還是集中在對Ruby 1.9的支援程度，對於新版Ruby中的細微改變都做了相對應的調整以求更好的整合，例如把**File.exists?**改為**File.exist?**。

另外，在Ruby 1.9中去掉了**Base64**模組(base64.rb)，因此在Rails中所有使用這個模組的都得修改為**ActiveSupport::Base64**。