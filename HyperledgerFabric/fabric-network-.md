## Organization

Trong mạng Hyperledger Fabric, organization (tạm dịch là tổ chức) là một khái niệm quan trọng để đại diện cho các thành viên trong mạng. Mỗi tổ chức thường đại diện cho một doanh nghiệp, một cơ quan hay một tổ chức khác trong thực tế.

Mỗi tổ chức trong mạng Fabric sẽ có một hoặc nhiều peer node (nút đồng thuận) để xử lý các giao dịch trong mạng. Các peer node của một tổ chức được quản lý bởi một MSP (Membership Service Provider), được sử dụng để quản lý các chứng chỉ và các chính sách liên quan đến quyền truy cập và xác thực.

Một mạng Fabric có thể bao gồm nhiều tổ chức khác nhau, mỗi tổ chức có thể có các quyền khác nhau trong việc thực hiện các giao dịch. Ví dụ, một tổ chức có thể có quyền tạo ra các giao dịch mới, trong khi một tổ chức khác chỉ có quyền xác thực các giao dịch.

Quyết định về cách tổ chức các thành viên trong mạng Fabric phụ thuộc vào cấu trúc tổ chức và yêu cầu kinh doanh của mỗi doanh nghiệp hay tổ chức sử dụng mạng này.

## Peer

Trong mạng Hyperledger Fabric, peer (nút đồng thuận) là một thành phần quan trọng để xử lý các giao dịch trong mạng. Peer đại diện cho các thành viên trong mạng, và thực hiện các chức năng như xác thực, đồng thuận và lưu trữ dữ liệu.

Có hai loại peer trong mạng Fabric:

1.  Endorsing peer (nút chứng thực): là peer thực hiện chức năng chứng thực giao dịch. Endorsing peer sẽ thực hiện xác nhận rằng giao dịch đã được chấp nhận và hợp lệ, sau đó chuyển cho ordering service (dịch vụ xếp thứ tự) để được xác nhận và đưa vào ledger (sổ cái) chính.
    
2.  Committing peer (nút xác nhận): là peer đóng vai trò trong việc xác nhận các giao dịch đã được chứng thực bởi endorsing peer. Committing peer sẽ lưu trữ các giao dịch được đưa vào ledger và xác nhận rằng các giao dịch đã được chấp nhận và đưa vào ledger chính.
    

Mỗi tổ chức trong mạng Fabric thường có một hoặc nhiều peer node để xử lý các giao dịch trong mạng. Các peer node của một tổ chức được quản lý bởi một MSP (Membership Service Provider), được sử dụng để quản lý các chứng chỉ và các chính sách liên quan đến quyền truy cập và xác thực.

## Certificate Authority

Trong mạng Hyperledger Fabric, CA (Certificate Authority) là một thành phần quan trọng để quản lý chứng chỉ số và xác thực các thành viên trong mạng.

CA đóng vai trò quan trọng trong việc tạo và phân phối các chứng chỉ số cho các thành viên trong mạng Fabric. Các chứng chỉ số này được sử dụng để xác thực và bảo mật các giao dịch trong mạng. Các CA thường được triển khai trên các node độc lập trong mạng hoặc trên các server quản lý tổ chức.

Các chứng chỉ số được tạo bởi CA sẽ được sử dụng để đăng ký và xác thực các thành viên trong mạng Fabric, bao gồm các peer, các orderer và các user. Việc xác thực các thành viên trong mạng sẽ giúp đảm bảo tính toàn vẹn và bảo mật của các giao dịch trong mạng.

Mỗi tổ chức trong mạng Fabric có thể có một hoặc nhiều CA, tùy thuộc vào cấu trúc tổ chức và yêu cầu kinh doanh của từng tổ chức. Các CA trong mạng Fabric có thể được triển khai dưới dạng CA độc lập hoặc CA liên kết với một tổ chức cụ thể.

Việc triển khai và quản lý các CA là rất quan trọng trong việc đảm bảo tính toàn vẹn và bảo mật của các giao dịch trong mạng Fabric.

## Membership Service Provider 

Trong mạng Hyperledger Fabric, MSP (Membership Service Provider) là một thành phần quan trọng để quản lý quyền truy cập và xác thực các thành viên trong mạng.

MSP đóng vai trò quan trọng trong việc xác thực và ủy quyền quyền truy cập cho các thành viên trong mạng Fabric. MSP quản lý các chứng chỉ số và các chính sách liên quan đến quyền truy cập và xác thực. Các thành viên trong mạng bao gồm các peer, các orderer và các user.

MSP đảm bảo rằng chỉ các thành viên được xác thực và có quyền truy cập mới có thể tham gia vào mạng Fabric và thực hiện các giao dịch trong mạng. Nó cũng đảm bảo rằng chỉ các peer và orderer được ủy quyền mới có thể tham gia vào việc xác nhận các giao dịch.

Mỗi tổ chức trong mạng Fabric có thể có một hoặc nhiều MSP, tùy thuộc vào cấu trúc tổ chức và yêu cầu kinh doanh của từng tổ chức. Các MSP có thể được triển khai dưới dạng MSP độc lập hoặc MSP liên kết với một tổ chức cụ thể.

Việc triển khai và quản lý các MSP là rất quan trọng trong việc đảm bảo tính toàn vẹn và bảo mật của các giao dịch trong mạng Fabric.

## Orderers

Trong mạng Hyperledger Fabric, orderers là một thành phần quan trọng trong quá trình xử lý và xác nhận các giao dịch trong mạng.

Orderers đóng vai trò quan trọng trong việc quản lý và xác nhận các giao dịch trong mạng Fabric. Các giao dịch được gửi đến orderers để được xác nhận và đóng gói thành các khối. Orderers sau đó sẽ phân phối các khối này đến các peer trong mạng Fabric để được xác nhận và lưu trữ.

Có hai loại orderers trong mạng Fabric: orderer đơn và orderer hợp tác. Orderer đơn là một orderer duy nhất, được triển khai để xử lý tất cả các giao dịch trong mạng. Orderer hợp tác được triển khai dưới dạng một nhóm các orderer làm việc cùng nhau để xác nhận các giao dịch và đảm bảo tính toàn vẹn của mạng.

Mạng Fabric cho phép triển khai nhiều orderer hợp tác và các orderer này có thể được phân bổ trên nhiều nút trong mạng. Các orderer hợp tác đảm bảo tính toàn vẹn của mạng bằng cách đồng bộ hóa các giao dịch và xác nhận các giao dịch được đóng gói trong các khối.

Việc triển khai và quản lý các orderer là rất quan trọng trong việc đảm bảo tính toàn vẹn và bảo mật của các giao dịch trong mạng Fabric.

## Channel

Trong mạng Hyperledger Fabric, channel là một khái niệm quan trọng để phân tách và quản lý quyền truy cập của các thành viên trong mạng.

Channel là một kênh truyền thông riêng tư trong mạng Fabric, được sử dụng để giới hạn quyền truy cập của các thành viên trong mạng đến các giao dịch cụ thể. Các channel được tạo ra để cho phép các tổ chức trong mạng Fabric thực hiện các giao dịch mà không cần chia sẻ thông tin với tất cả các thành viên trong mạng.

Mỗi channel trong mạng Fabric có các thành viên và orderers được ủy quyền, chỉ các thành viên và orderers này mới có thể tham gia vào các giao dịch trong channel. Các channel có thể được tạo ra để cho phép các tổ chức trong mạng Fabric thực hiện các giao dịch riêng tư mà không cần chia sẻ thông tin với các tổ chức khác trong mạng.

Việc sử dụng các channel trong mạng Fabric giúp đảm bảo tính riêng tư và an toàn của các giao dịch, đồng thời giảm thiểu rủi ro từ các phản ứng không mong muốn của các thành viên trong mạng. Ngoài ra, các channel còn giúp mạng Fabric mở rộng dễ dàng hơn bằng cách tăng khả năng xử lý giao dịch và giảm thiểu độ trễ trong việc xử lý các giao dịch.

Việc quản lý và cấu hình các channel là rất quan trọng trong việc đảm bảo tính toàn vẹn và bảo mật của các giao dịch trong mạng Fabric.
