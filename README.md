# AWS-overview
## Terms
* ACL(Access Control List,)
* AMI(Amazon Machine Image)
* ARN(Amazon Resource Name)
* AZ(Available Zone, 可用區域)
* EBS(Elastic Block Store)
* EC2(Elastic Compute Cloud)
* ECR(Elastic Container Registry)
* ECS(Elastic Container Service)
* ELB(Elastic Load Balancing)
* IAM(Identity and Access Management)
* MFA(MultiFactor Authentication)
* RDS(Relational Database Service)
* S3(Simple Storage Service)
* SNS(Simple Notification Service)
* VPC(Virtual Private Cloud, 虛擬私有雲端)
## EC2 (Elastic Compute Cloud)
### What is EC2
https://docs.aws.amazon.com/zh_tw/AWSEC2/latest/UserGuide/concepts.html
Amazon EC2 提供以下功能：

* 虛擬運算環境，亦即執行個體
* 供執行個體使用的預先設定範本，亦即 Amazon Machine Images (AMI)，在其中封裝伺服器所需的元件 (包括作業系統和其他軟體)
* 執行個體 CPU、記憶體、儲存和聯網功能的各種組態，亦即執行個體類型
* 使用金鑰對來保護執行個體的登入資訊 (AWS 會存放公有金鑰，而您則於安全位置存放私有金鑰)
* 儲存磁碟區可供您停止或終止執行個體所刪除的暫時性資料使用，亦即執行個體存放磁碟區
* 資料的持久性儲存磁碟區請使用 Amazon Elastic Block Store (Amazon EBS)，亦即 Amazon EBS 磁碟區
* 供資源 (如執行個體和 Amazon EBS 磁碟區) 使用的多個實體位置，亦即區域和可用區域
* 防火牆，讓您可指定通訊協定、連接埠，以及能夠使用安全群組前往執行個體的來源 IP 範圍
* 可供動態雲端運算使用的靜態 IPv4 地址，亦即彈性 IP 地址
* 中繼資料亦即標籤，您可建立標籤並將其指派至 Amazon EC2 資源
* 您可建立的虛擬網路，亦即虛擬私有雲端 (VPC)，這些網路在邏輯上與 AWS 雲端上的其他網路隔離，您可選擇將其連接至您自己的網路
### What can we do with EC2
可以將 EC2 視為 Amazon 所提供的線上虛擬機器，透過使用者金鑰可從本機端連線至 Amazon 線上服務的虛擬機中進行各式操作，在虛擬機的作業系統部分，可透過 Amzon 所提供的 AMI （如 Windows, Ubuntu, Red Hat等）選擇偏好的作業系統，並為這些虛擬機配置自己所需的服務。
## ECS (Elastic Container Service)
### What is ECS
ECS 是具高可擴展性且快速的容器管理服務，可以在叢集上輕鬆執行、停止和管理 Docker 容器。可以使用 Fargate 啟動類型或 EC2 啟動類型進行服務或任務，兩者最大的差異為 Fargate 可以無需管理底層節點而運行你的 Docker 容器
Fargate 運作方式如下圖：
![](https://i.imgur.com/EPpnILw.png)
運行 ECS 前需先進行任務定義，說明配置應用程式的一或多個容器設置
### What can we do whit ECS
在概念上可將 ECS 比擬為 Docker 所應用到的 Docker-compose 配置服務，透過建立一個 Cluster（如同 Docker Stack 概念）並建立各個 Task difinition（如同 Docker compose file），在 Task difintion 中可，可將設定好的 Task difinition 配置到各個 Cluster 之中，ECS 將會根據 Task difinition 內容配置微服務並保證其運行。

## IAM (Identity and Access Management)
在最初申請 AWS 服務時使用 e-mail 申請的帳號為 Root account，擁有該帳戶的最大權限，但隨著開發者所需的服務越來越多，同時也意味著需要更多的管理者，因此在多人協作上就會用到 AWS 所提供的 IAM 服務，讓其他人能以適當的權限登入並進行操作。
IAM 用來提供各種對 AWS 資源的存取的安全控管機制。可以使用 IAM 來控制 (已登入) 的身分驗證和授權使用資源的 (許可)
* 共用存取您的 AWS 帳戶
可以授予其他人管理和使用 AWS 帳戶資源的許可，而無需共用密碼或存取金鑰。
* 精準的許可
對不同的人員授予不同資源的不同許可。例如，您可能允許一些使用者完整存取 Amazon Elastic Compute Cloud (Amazon EC2)、Amazon Simple Storage Service (Amazon S3)、Amazon DynamoDB、Amazon Redshift 和其他 AWS 服務。對於其他使用者，您可以只允許對一些 S3 儲存貯體進行唯讀存取，或僅允許管理一些 EC2 執行個體，或存取您的帳單資訊，但不能進行任何其他動作。
* 提供兩步驟驗證(Multi-factor authentication, MFA)
可以為帳戶和個別使用者新增雙重身分驗證，以提高安全性。使用MFA，使用者不僅必須提供密碼或存取金鑰才能使用帳戶，還必須提供來自特殊設定裝置的代碼。
IAM 上的名詞基本介紹:
* User(終端使用者)
可以將這此視為使用者登入帳戶
* Groups(群組)
可以建立一個特定的群組並設定一組權限給一群特定的使用者（如管理員權限等）
* Roles(角色)
可以透過角色賦予給 AWS 的服務與其他資源的存取權限並這定至該角色上，如可將角色設定權限為能夠存取 ECR 並將此角色賦予給 ECS 使用，如此一來 ECS 就能擁有存取 ECR 上的 Image 權限
* Policies(策略方針)
可以透過此方式來制定一組設定檔來定義一至多個權限，角色可直接選用這些策略方針
![](https://i.imgur.com/4eLwrse.png)

在 Root account 底下可新增使用者（User），可設定該使用這所需求的存取方式：程式設計方式存取（主要為 CLI 介面）以及 AWS Management Console 存取（主要為網頁 GUI 介面）；使用程式設計方式存取，系統會自動隨機產生出一組 Access Key ID 以及 Secret Access Keys 供使用在 AWS CLI 或是使用 AWS SDK 登入時做為登入密碼使用，須注意此 Key pair 只會在系統隨機產生當下顯示，之後無法透過查詢得知該 Secret Access Keys，若忘記 Secret Access Keys 時的處置方式只能特過刪除舊有 Key pair 並重新產生一組新的 Key pair；使用 AWS Management Console 存取則如同 Root account 一般，透過限縮並配置適當的權限，使用者可以登入 AWS Management Console 並進行操作。

## RDS (Relational Database Service)
RDS 是 AWS 雲端中關聯式資料庫的設定、操作和擴展更加簡單。其能為產業標準的關聯式資料庫提供具成本效益、可調整大小的容量，並管理常見的資料庫管理任務。
* 可輕鬆配置選用所需的資源，如 CPU、記憶體、儲存空間和 IOPS
* RDS 會管理備份、軟體修補、自動故障偵測與復原作業。
* 可在需要時執行自動備份，或自行手動建立備份快照
* 發生問題時，有主要執行個體與同步次要執行個體可以容錯移轉，從而享有高可用性。支援多個 AZ 佈署的 RDS Replication 服務，當主要執行個體故障後會自動切換到次要執行個體
## ECR (Elastic Container Registry)
ECR 為 AWS Docker 的登錄檔服務，具安全性、可擴展性和可靠性。Amazon ECR 支援使用 AWS IAM 資源型許可的私有 Docker 儲存庫，所以特定的使用者或 Amazon EC2 執行個體可以存取儲存庫和映像。開發人員可以使用 Docker CLI 來推送、提取和管理映像檔。
## S3 (Simple Storage Service)
S3 服務的特性：
* S3是物件檔案儲存服務
* 單一物件的大小最高可達 5 TB
* 將最多 10 個金鑰值對 (稱為 S3 物件標籤) 附加至物件
* 檔案會上傳至指定的儲存貯體（Bucket）
* 可進行靜態網站託管託管
* 可進行儲存貯體政策編輯（如限制誰可對該儲存貯體進行存取）
* CORS 組態編輯（有跨來源資源共享需求時可針對網域及Method進行設定）
* 可以針對檔案的生命週期做管理（詳見 https://docs.aws.amazon.com/zh_tw/AmazonS3/latest/user-guide/create-lifecycle.html ）

## VPC (Virtual Private Cloud)
Amazon VPC 是 Amazon EC2 的 networking layer，VPC 的重要概念：
* 虛擬私有雲端 (VPC) 是您 AWS 帳戶專用的虛擬網路。
* 子網路是您的 VPC 中的 IP 地址範圍。
* 路由表包含一組名為路由的規則，用來判斷網路流量的方向。
* 網際網路閘道是一種水平擴展、備援且高可用性的 VPC 元件，允許 VPC 中執行個體與網際網路之間的通訊。因此不會對網路流量強加可用性風險或頻寬限制。
* VPC 端點可讓您將 VPC 私下連線至支援的 AWS 服務以及具有 PrivateLink 功能的 VPC 端點服務，而不需要網際網路閘道、NAT 裝置、VPN 連線或 AWS Direct Connect 連線。VPC 中的執行個體不需要公有 IP 地址，即可與服務中的資源通訊。VPC 與另一個服務之間的流量都會保持在 Amazon 網路的範圍內。
## ELB (Elastic Load Balancing)
### Application Load Balancer
在請求層 (Layer 7) 運作，根據請求的內容將流量路由到目標 – EC2 執行個體、容器、IP 地址和 Lambda 函數。Application Load Balancer 適合用於 HTTP 和 HTTPS 流量的進階負載平衡，它針對現代應用程式架構 (包括微型服務和以容器為基礎的應用程式) 提供進階的請求路由。Application Load Balancer 透過一律使用最新的 SSL/TLS 加密技術和協定，以簡化和改進應用程式的安全性。
![](https://i.imgur.com/5YIGBYt.png)

### Network Load Balancer
在連線層 (Layer 4) 運作，根據 IP 協定資料將連線路由至 Amazon Virtual Private Cloud (Amazon VPC) 中的目標 – Amazon EC2 執行個體、微型服務和容器。Network Load Balancer 適合用於 TCP 和 UDP 流量的負載平衡，每秒能夠處理數百萬個請求，同時保持超低延遲。網路負載平衡器已經過優化，在每個可用區域中使用單一靜態 IP 地址即可處理突發與臨時性的流量模式。它已經與其他熱門 AWS 服務整合，例如 Auto Scaling、Amazon EC2 Container Service (ECS)、Amazon CloudFormation 和 AWS Certificate Manager (ACM)。
### Classic Load Balancer
提供跨多個 Amazon EC2 執行個體的基本負載平衡功能，而且可同時在請求層與連線層運作。Classic Load Balancer 適用於在 EC2-Classic 網路內建立的應用程式。使用 Virtual Private Cloud (VPC) 時，建議使用 Layer 7 的 Application Load Balancer 和 Layer 4 的 Network Load Balancer。
![](https://i.imgur.com/1zkM2OK.png)
## Reference
[AWS Documentation](https://docs.aws.amazon.com/)
## License
MIT license
