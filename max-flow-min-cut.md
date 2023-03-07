## Giới thiệu bài toán

Bài toán luồng cực đại và lát cắt cực tiểu là hai bài toán quan trọng trong lý thuyết đồ thị. Bài toán luồng cực đại đặt ra câu hỏi tìm cách truyền dữ liệu từ nguồn đến đích sao cho lượng dữ liệu truyền được là lớn nhất, trong khi đó bài toán lát cắt cực tiểu tìm cách cắt đồ thị thành hai phần sao cho tổng trọng số của các cạnh bị cắt là nhỏ nhất. Cả hai bài toán này đều được ứng dụng rộng rãi trong thực tiễn, ví dụ như trong mạng lưới giao thông, mạng máy tính, quản lý tài nguyên nước và điện. Giải quyết thành công các bài toán này không chỉ giúp tối ưu hóa hoạt động mà còn giúp đưa ra những quyết định đúng đắn và chính xác.

Để giải quyết bài toán luồng cực đại và lát cắt cực tiểu, các nhà nghiên cứu đã đưa ra nhiều phương pháp khác nhau. Phương pháp cơ bản nhất là phương pháp `Ford-Fulkerson`, là phương pháp tham lam (greedy) cập nhật luồng trên một đường tăng trọng số (augmenting path) trong mạng, đến khi không còn đường tăng trọng số nào nữa. Ngoài phương pháp `Ford-Fulkerson`, còn có các phương pháp giải khác như `Edmonds-Karp`, `Dinic's Algorithm`, `Push-Relabel Algorithm` và `Capacity Scaling`.

Bài toán luồng cực đại và lát cắt cực tiểu có nhiều ứng dụng trong thực tế. Ví dụ, chúng được sử dụng để mô hình hóa dòng chảy trong một mạng lưới vận tải hoặc lưu lượng trong một mạng máy tính. Bài toán này cũng được sử dụng trong quản lý tài nguyên nước và điện, nơi việc tối ưu hóa luồng nước hoặc điện là rất quan trọng. Ngoài ra, các bài toán này còn được sử dụng trong lĩnh vực tối ưu hóa để tìm kiếm các giải pháp tối ưu cho các vấn đề tương tự.

## Giải quyết bài toán

### Một sô khái niệm

**Đồ thị (Graph)**

Là một cấu trúc dữ liệu trừu tượng được sử dụng để mô hình hóa các mối quan hệ giữa các đối tượng. Nó được biểu diễn bởi một tập hợp các đỉnh (vertices) và các cạnh (edges) nối các đỉnh này với nhau.

Một cạnh (edge) trong đồ thị có thể có hướng hoặc không hướng. Nếu cạnh có hướng, ta gọi nó là đồ thị có hướng (directed graph), ngược lại, nếu cạnh không hướng thì ta gọi nó là đồ thị vô hướng (undirected graph). Mỗi cạnh có thể được gán trọng số (weight), thể hiện sự liên kết hay khoảng cách giữa các đỉnh.

Các đồ thị có thể được sử dụng để mô hình hóa rất nhiều vấn đề khác nhau trong đó các đỉnh đại diện cho các thực thể và các cạnh đại diện cho các mối quan hệ giữa chúng. Ví dụ, trong mạng lưới giao thông, các nút có thể đại diện cho các thành phố và các cạnh có thể đại diện cho các tuyến đường nối các thành phố với nhau. Trong mạng lưới điện, các nút có thể đại diện cho các trạm điện và các cạnh có thể đại diện cho các đường dây điện nối các trạm với nhau.

**Luồng (Flow)**

Là một khái niệm trong lý thuyết đồ thị, thường được áp dụng trong bài toán lưu lượng (flow problem) như bài toán lưu lượng cực đại (maximum flow problem).

Trên một đồ thị có hướng G = (V, E), với các cạnh có khả năng chứa một lượng lưu lượng (flow) từ một đỉnh đến đỉnh khác, một luồng f được định nghĩa là một phân bố các lưu lượng trên các cạnh của đồ thị sao cho:

1.  Đối với mọi cạnh (u, v) ∈ E, lượng lưu lượng f(u,v) không vượt quá giới hạn của cạnh (có thể hiểu là độ rộng của ống dẫn, hoặc dung tích của ống dẫn).
2.  Đối với mọi đỉnh u ∈ V{s,t}, tổng lưu lượng đi vào đỉnh đó bằng tổng lưu lượng đi ra khỏi đỉnh đó (tức là lưu lượng không bị tồn đọng tại đỉnh đó).
3.  Lưu lượng đi qua cạnh không âm (f(u,v) >= 0).

Để tìm giá trị luồng cực đại (*Maximum flow*) trên đồ thị, chúng ta cần tìm một luồng sao cho tổng lượng lưu lượng từ đỉnh nguồn (s) đến đỉnh đích (t) là lớn nhất.

**Lát cắt (Cut)**

Trong đồ thị, một lát cắt (cut) là một tập hợp các đỉnh được phân chia thành hai tập con không trùng nhau, thường được gọi là tập S và tập T. Lát cắt S-T là tập hợp của tất cả các cạnh nối từ tập S đến tập T.

**Lát cắt cực tiểu (Minimum cut)**

Lát cắt cực tiểu (Minimum cut) trên một đồ thị là một lát cắt có tổng trọng số của các cạnh trong lát cắt là nhỏ nhất so với tất cả các lát cắt khác trên đồ thị đó. Trong lý thuyết đồ thị, một lát cắt thường được định nghĩa là sự phân chia đồ thị thành hai tập con S và T, sao cho đỉnh nguồn s nằm trong tập S và đỉnh đích t nằm trong tập T. Trọng số của một lát cắt được tính bằng tổng trọng số của các cạnh xuất phát từ các đỉnh thuộc tập S và kết thúc tại các đỉnh thuộc tập T.

Việc tìm lát cắt cực tiểu trên một đồ thị rất quan trọng trong nhiều ứng dụng, như tìm đường cắt tỉa nhỏ nhất trong mạng lưới viễn thông, tìm đường cắt tỉa nhỏ nhất trong mạng chuyển tiền, tìm lát cắt tối ưu trong phân cụm, tìm các bộ phân chia hợp lý trong định lượng nguồn lực, v.v.

**Đường tăng luồng (Augmenting path)**

Là đường đi từ đỉnh nguồn đến đỉnh đích trên đồ thị có thể chứa các cạnh được tăng giá trị luồng, tăng giá trị luồng của mỗi cạnh bằng lượng tối đa có thể được tăng.

Một đường tăng luồng được tạo ra bằng cách sử dụng một thuật toán tìm kiếm đường đi như DFS hoặc BFS. Khi một đường tăng luồng được tìm thấy, lượng luồng tối đa có thể được tăng trên đường đó bằng lượng luồng còn lại trên đường tăng luồng (bottleneck capacity).

Ví dụ, trên một đồ thị có các đỉnh và các cạnh được gán trọng số và mỗi cạnh có một giá trị luồng tối đa, đường tăng luồng giữa đỉnh nguồn và đỉnh đích có thể được tìm bằng cách tìm kiếm đường đi từ đỉnh nguồn đến đỉnh đích. Sau đó, lượng luồng trên đường đó có thể được tăng bằng lượng luồng tối đa có thể được tăng trên đường đó.

**Phân lớp mạng (layered network)**

Là một kỹ thuật được sử dụng trong thuật toán Dinic để tìm đường tăng trọng số (augmenting path) trên đồ thị. Kỹ thuật này tạo ra một mạng phụ mới dựa trên đồ thị gốc, trong đó các đỉnh được phân loại vào các tầng (layer) khác nhau, tương tự như việc phân loại các tầng của một tòa nhà.

Cụ thể, phân lớp mạng xác định một tập các tầng trên đồ thị ban đầu, trong đó tầng đầu tiên chứa đỉnh nguồn và tầng cuối cùng chứa đỉnh đích. Các tầng khác nằm giữa hai tầng này và được xác định bởi khoảng cách tối thiểu từ đỉnh nguồn. Điều này có nghĩa là các đỉnh nằm cách đỉnh nguồn một bước sẽ được phân loại vào tầng thứ hai, các đỉnh nằm cách đỉnh nguồn hai bước sẽ được phân loại vào tầng thứ ba, và tiếp tục như vậy. Các đỉnh không thể truy cập từ đỉnh nguồn sẽ không thuộc vào bất kỳ tầng nào.

Sau khi tạo ra phân lớp mạng, thuật toán Dinic sử dụng nó để tìm đường tăng trọng số. Thuật toán sẽ tìm kiếm các đường đi từ đỉnh nguồn đến đỉnh đích theo thứ tự các tầng, bắt đầu từ các đỉnh ở tầng đầu tiên và di chuyển đến các đỉnh ở tầng tiếp theo. Đường đi được tìm thấy sẽ là đường tăng trọng số nếu tất cả các cạnh trên đường đều chưa đầy đủ. Nếu không có đường tăng trọng số nào khả dụng, thuật toán sẽ kết thúc và trả về luồng cực đại trên đồ thị.

**Residual graph**
Residual graph là đồ thị tương ứng với đồ thị ban đầu khi ta đang thực hiện thuật toán tìm luồng cực đại. Trong residual graph, các cạnh của đồ thị gốc được chia thành hai loại:

*   Các cạnh mang lại khả năng tăng luồng (còn được gọi là cạnh forward hoặc cạnh thuận).
*   Các cạnh mang lại khả năng giảm luồng (còn được gọi là cạnh backward hoặc cạnh nghịch).

Các cạnh forward có trọng số bằng khả năng tăng luồng còn các cạnh backward có trọng số bằng khả năng giảm luồng.

Trong quá trình tìm luồng cực đại, ta cập nhật residual graph theo từng bước, dựa trên đường tăng luồng mà thuật toán tìm được. Cụ thể, ta tăng trọng số của các cạnh forward trên đường tăng luồng và giảm trọng số của các cạnh backward trên đường tăng luồng. Sau mỗi lần cập nhật residual graph, thuật toán tiếp tục tìm đường tăng luồng trên đồ thị mới này. Quá trình này tiếp tục cho đến khi không còn đường tăng luồng nào trên residual graph, tức là đã tìm được luồng cực đại trên đồ thị gốc.

**Độ dư (Residual capacity)**

Là lượng luồng còn lại có thể đi qua một cạnh sau khi một luồng đã được truyền qua cạnh đó ( Một số tài liệu sẽ gọi là giá trị thặng dư ).

### Một số thuật toán

#### Thuật toán Ford-Fulkerson

Thuật toán Ford-Fulkerson là một thuật toán tìm kiếm theo chiều sâu (DFS) và không được đảm bảo hoạt động chính xác trên đồ thị có trọng số âm. Điều này là do khi tìm đường tăng luồng trên đồ thị có trọng số âm, thuật toán có thể bị mắc kẹt trong vòng lặp vô hạn, dẫn đến không tìm được kết quả đúng.

Dưới đây là mô tả sơ lược về cách thức giải quyết bài toán bằng thuật toán Ford-Fulkerson:

**Tìm luồng cực đại**

1.  Khởi tạo luồng ban đầu bằng 0.
2.  Tìm một đường đi từ đỉnh nguồn tới đỉnh đích trong đồ thị.
3.  Tìm luồng nhỏ nhất trên đường đi vừa tìm được.
4.  Tăng luồng trên các cạnh trên đường đi đó bằng lượng luồng nhỏ nhất vừa tìm được.
5.  Lặp lại bước 2 đến khi không còn đường đi nào từ đỉnh nguồn tới đỉnh đích trong đồ thị.

**Tìm lát cắt cực tiểu**

Sau khi thực hiện thuật toán Ford-Fulkerson để tìm luồng cực đại, ta có thể sử dụng một số phương pháp khác để tìm lát cắt cực tiểu.

Một phương pháp đơn giản là sử dụng thuật toán DFS để tìm các đỉnh nằm trong lát cắt. Cụ thể: 

1. Khởi tạo tập `S` bằng đỉnh source và tập `T` bằng toàn bộ các đỉnh còn lại trong đồ thị.
2. Khởi tạo mảng `visited` với giá trị `False` tương ứng với tất cả các đỉnh.
3. Thực hiện DFS trên đỉnh nguồn, đánh dấu visited cho các đỉnh được truy cập.
4. Với mỗi đỉnh `u` đã được truy cập và có cạnh nối đến một đỉnh v chưa được truy cập và có trọng số dương, ta đưa `v` vào tập `S`.
5. Lặp lại bước 3 và 4 cho đến khi không còn đỉnh nào được thăm.
6. Lát cắt cực tiểu là cạnh giữa tập `S` và tập `T`.

Tuy nhiên, phương pháp này không hiệu quả với đồ thị có nhiều đỉnh và cạnh.

**Mã giả**

Đây là mã giả của thuật toán **Ford-Fulkerson** để tìm luồng cực đại trên đồ thị có hướng và có trọng số dương.

```
function FordFulkerson(graph, source, sink):
    // Khởi tạo luồng ban đầu là 0
    maxFlow = 0
    
    // Vòng lặp chính của thuật toán
    while (true):
        // Khởi tạo mảng visited để lưu trạng thái duyệt của các đỉnh
        visited = [false, ..., false]
        
        // Khởi tạo mảng parent để lưu trạng thái của đường đi
        parent = [-1, ..., -1]
        
        // Khởi tạo hàng đợi để lưu các đỉnh cần duyệt
        queue = []
        
        // Đưa đỉnh nguồn vào hàng đợi
        queue.push(source)
        visited[source] = true
        
        // Vòng lặp BFS để tìm đường tăng luồng
        while (len(queue) > 0):
            u = queue.pop(0)
            for v in graph[u]:
                if not visited[v] and graph[u][v] > 0:
                    visited[v] = true
                    parent[v] = u
                    queue.push(v)
        
        // Nếu không còn đường tăng luồng nữa thì thoát vòng lặp
        if not visited[sink]:
            break
        
        // Tìm giá trị tăng luồng
        flow = float("inf")
        v = sink
        while (v != source):
            u = parent[v]
            flow = min(flow, graph[u][v])
            v = u
        
        // Cập nhật đồ thị và luồng
        v = sink
        while (v != source):
            u = parent[v]
            graph[u][v] -= flow
            graph[v][u] += flow
            v = u
        maxFlow += flow
    
    // Trả về luồng cực đại
    return maxFlow
```

Trong đó:

*   `graph` là ma trận trọng số của đồ thị
*   `source` là đỉnh nguồn
*   `sink` là đỉnh đích
*   `visited` là mảng lưu trạng thái duyệt của các đỉnh
*   `parent` là mảng lưu trạng thái của đường đi
*   `queue` là hàng đợi để lưu các đỉnh cần duyệt
*   `maxFlow` là giá trị luồng cực đại

Và mã giả cho phương pháp tìm lát cắt cực tiểu bằng thuật toán DFS

```
function find_min_cut_DFS(graph, source, sink):
    // Khởi tạo tập S bằng đỉnh nguồn và tập T bằng toàn bộ các đỉnh còn lại
    S = [source]
    T = [v for v in graph if v != source]

    // Khởi tạo visited với giá trị False tương ứng với tất cả các đỉnh
    visited = {v: False for v in graph}

    // Thực hiện DFS trên đỉnh nguồn
    stack = [source]
    while stack:
        u = stack.pop()
        visited[u] = True
        for v, w in graph[u]:
            if not visited[v] and w > 0:
                stack.append(v)

    // Duyệt qua tất cả các đỉnh đã được thăm và có cạnh nối đến một đỉnh chưa được thăm và có trọng số dương
    for u in visited:
        if visited[u]:
            for v, w in graph[u]:
                if not visited[v] and w > 0:
                    // Đưa đỉnh v vào tập S
                    S.append(v)

    // Lát cắt cực tiểu là cạnh giữa tập S và tập T
    min_cut = []
    for u in S:
        for v, w in graph[u]:
            if v in T:
                min_cut.append((u, v, w))

    return min_cut
```

Trong đó:

*   `graph` là danh sách kề của đồ thị
*   `source` là đỉnh nguồn
*   `sink` là đỉnh đích

Lưu ý rằng mã giả này giả sử đồ thị được biểu diễn dưới dạng danh sách kề. Nếu đồ thị được biểu diễn bằng ma trận kề, cần sử dụng một số biến thay thế để lưu trữ thông tin về các đỉnh và cạnh.

#### Thuật toán Edmonds-Karp

Thuật toán Edmonds-Karp là một thuật toán giải bài toán luồng cực đại và lát cắt cực tiểu trên đồ thị có hướng và có trọng số dương. Đây là một thuật toán tối ưu về mặt thời gian so với thuật toán Ford-Fulkerson.

Thuật toán Edmonds-Karp đảm bảo cho kết quả chính xác cho bài toán luồng cực đại và lát cắt cực tiểu trên đồ thị có hướng và có trọng số dương. Đồng thời, nó cũng đảm bảo thời gian chạy tối ưu hơn so với thuật toán Ford-Fulkerson.

Tuy nhiên, cũng tương tự như thuật toán Ford-Fulkerson, thuật toán Edmonds-Karp cũng không được đảm bảo hoạt động chính xác trên đồ thị có trọng số âm. Điều này là do thuật toán Edmonds-Karp sử dụng phương pháp tìm kiếm theo chiều rộng (BFS) để tìm đường tăng luồng, và việc sử dụng phương pháp này trên đồ thị có trọng số âm có thể dẫn đến kết quả không chính xác.


Dưới đây là các bước giải quyết bài toán luồng cực đại và lát cắt cực tiểu bằng thuật toán Edmonds-Karp:

**Tìm luồng cực đại**

1.  Khởi tạo luồng ban đầu bằng 0.
2.  Tìm một đường đi từ đỉnh nguồn tới đỉnh đích trong đồ thị bằng thuật toán tìm kiếm theo chiều rộng (BFS).
3.  Tìm luồng nhỏ nhất trên đường đi vừa tìm được.
4.  Tăng luồng trên các cạnh trên đường đi đó bằng lượng luồng nhỏ nhất vừa tìm được.
5.  Lặp lại bước 2 và 4 cho đến khi không còn đường đi nào từ đỉnh nguồn tới đỉnh đích trong đồ thị.

**Tìm lát cắt cực tiểu**

Sau khi tìm được luồng cực đại bằng thuật toán Edmonds-Karp, ta có thể tìm các cạnh nối giữa các đỉnh thuộc phần đồ thị chứa đỉnh nguồn và phần đồ thị chứa đỉnh đích. Lát cắt cực tiểu chính là tổng trọng số của các cạnh nối các đỉnh này. Cụ thể như sau:

1.  Khởi tạo tập S bằng đỉnh nguồn (source) và tập T bằng tất cả các đỉnh còn lại trong đồ thị.
2.  Sử dụng thuật toán DFS hoặc BFS để tìm các đỉnh mà có thể được truy cập từ đỉnh nguồn.
3.  Tất cả các đỉnh được truy cập bởi thuật toán DFS hoặc BFS sẽ thuộc vào tập S.
4.  Các đỉnh còn lại thuộc vào tập T.
5.  Lát cắt cực tiểu là tập các cạnh mà bắt đầu từ các đỉnh trong tập S và kết thúc tại các đỉnh trong tập T.

Lưu ý rằng tập S và T có thể được xác định bằng cách sử dụng đồ thị phụ thuộc vào luồng cực đại. Các đỉnh trong tập S là các đỉnh mà có thể được truy cập từ đỉnh nguồn bằng các cạnh có khả năng chưa đầy đủ. Các đỉnh còn lại thuộc tập T.

**Mã giả**

Đây là mã giả của thuật toán Edmonds-Karp để tìm luồng cực đại trên đồ thị có hướng và có trọng số dương.

```
Edmonds-Karp(graph, source, sink):
    for each edge (u, v) in graph:
        set f(u, v) = 0     // Khởi tạo luồng trên tất cả các cạnh bằng 0
    
    while true:
        queue = []          // Khởi tạo hàng đợi rỗng
        dist = []           // Khởi tạo mảng lưu khoảng cách
        
        for each vertex v in graph:
            dist[v] = infinity  // Khởi tạo khoảng cách của mỗi đỉnh bằng vô cùng
        
        dist[source] = 0         // Khoảng cách từ đỉnh nguồn đến chính nó là 0
        queue.append(source)     // Thêm đỉnh nguồn vào hàng đợi
        
        while queue is not empty:
            u = queue.pop(0)        // Lấy đỉnh u ra khỏi hàng đợi
            for each neighbor v of u:
                if f(u, v) < c(u, v) and dist[v] > dist[u] + 1:
                    f(u, v) = f(u, v) + 1   // Tăng luồng trên cạnh (u, v) lên 1
                    f(v, u) = f(v, u) - 1   // Giảm luồng trên cạnh (v, u) đi 1
                    dist[v] = dist[u] + 1   // Cập nhật khoảng cách
                    queue.append(v)         // Thêm đỉnh v vào hàng đợi
        
        if dist[sink] == infinity:     // Nếu đỉnh đích không thể đến được từ đỉnh nguồn thì thoát vòng lặp
            break
    
    max_flow = 0
    for each neighbor v of source:
        max_flow = max_flow + f(source, v)   // Tổng luồng trên tất cả các cạnh đi ra từ đỉnh nguồn
    
    return max_flow   // Trả về giá trị luồng cực đại
```

Trong đó:

*   `graph` là ma trận trọng số của đồ thị
*   `source` là đỉnh nguồn
*   `sink` là đỉnh đích

Và mã giả cho phương pháp tìm lát cắt cực tiểu sau khi tìm luồn cực đại bằng Edmonds-Karp

```
// Tìm lát cắt cực tiểu sau khi tìm luồn cực đại bằng Edmonds-Karp
function min_cut(graph, source, sink, flow):
    // Khởi tạo tập S bằng đỉnh nguồn và tập T bằng tất cả các đỉnh còn lại
    S = set()
    T = set(graph.keys()) - S.add(source)

    // Sử dụng BFS để tìm các đỉnh trong tập S
    visited = {v: False for v in graph.keys()}
    q = [source]
    visited[source] = True
    while q:
        u = q.pop(0)
        for v, capacity in graph[u].items():
            if not visited[v] and capacity - flow[(u, v)] > 0:
                visited[v] = True
                q.append(v)
                S.add(v)

    // Lát cắt cực tiểu là tập các cạnh bắt đầu từ các đỉnh trong tập S và kết thúc tại các đỉnh trong tập T.
    cut_edges = set()
    for u in S:
        for v in graph[u].keys():
            if v in T:
                cut_edges.add((u, v))

    return cut_edges
```

Trong đó:

*   `graph` là ma trận trọng số của đồ thị
*   `source` là đỉnh nguồn
*   `sink` là đỉnh đích
*   `f(u, v)` à giá trị luồng trên cạnh từ đỉnh `u` đến đỉnh `v`
*   `c(u, v)` là giá trị trọng số trên cạnh từ đỉnh `u` đến đỉnh `v`
*   `dist[v]` là khoảng cách từ đỉnh nguồn đến đỉnh `v`.
*   `queue` là hàng đợi để lưu các đỉnh cần duyệt
*   `maxFlow` là giá trị luồng cực đại

Lưu ý rằng mã giả này giả sử đồ thị được biểu diễn dưới dạng danh sách kề. Nếu đồ thị được biểu diễn bằng ma trận kề, cần sử dụng một số biến thay thế để lưu trữ thông tin về các đỉnh và cạnh.

#### Thuật toán Dinic

Thuật toán Dinic là một thuật toán khác để giải bài toán luồng cực đại và lát cắt cực tiểu trên đồ thị có hướng và có trọng số dương. Thuật toán này sử dụng phương pháp phân lớp mạng (layered network) để tối ưu hóa quá trình tìm luồng cực đại trên đồ thị.

Tương tự như thuật toán Ford-Fulkerson và thuật toán Edmonds-Karp, thuật toán Dinic cũng không được đảm bảo hoạt động chính xác trên đồ thị có trọng số âm.Tuy nhiên, thuật toán Dinic có một số đặc tính đặc biệt giúp nó hoạt động hiệu quả trên các đồ thị có cấu trúc đặc biệt, bao gồm đồ thị có bậc vào và bậc ra của các đỉnh bằng nhau, hay đồ thị không có chu trình âm. Tuy nhiên, trên các đồ thị có trọng số âm, việc sử dụng thuật toán Dinic vẫn có thể dẫn đến kết quả không chính xác.

Thuật toán Dinic sử dụng phương pháp tìm kiếm theo chiều rộng (BFS) để tìm đường tăng luồng. Sau khi tìm được đường tăng luồng, giá trị luồng của đường đó được cập nhật và cứ như vậy, thuật toán tiếp tục tìm đường tăng luồng cho đến khi không còn đường tăng luồng nữa.

Với độ phức tạp là O(V^2E) trong trường hợp tổng số đường đi tăng luồng lớn, thuật toán Dinic thường được sử dụng để giải quyết bài toán luồng cực đại trên các đồ thị có kích thước nhỏ và có cấu trúc đặc biệt, chẳng hạn như trong các ứng dụng mạng máy tính.

Thuật toán Dinic đảm bảo cho kết quả chính xác cho bài toán luồng cực đại và lát cắt cực tiểu trên đồ thị có hướng và có trọng số dương. Đồng thời, nó cũng đảm bảo thời gian chạy tối ưu hơn so với thuật toán Edmonds-Karp trên một số trường hợp.

Dưới đây là các bước giải quyết bài toán luồng cực đại và lát cắt cực tiểu bằng thuật toán Dinic:

**Tìm luồng cực đại**

1.  Khởi tạo luồng ban đầu bằng 0.
2.  Tạo một mạng con (residual network) trên đồ thị với trọng số còn lại trên mỗi cạnh là bằng trọng số gốc trừ đi luồng hiện tại.
3.  Sử dụng thuật toán tìm kiếm theo chiều rộng (BFS) để tìm một đường tăng trong mạng con.
4.  Nếu không tìm được đường tăng nào nữa, kết thúc thuật toán.
5.  Nếu tìm được đường tăng, tính luồng nhỏ nhất trên đường tăng đó.
6.  Tăng luồng trên các cạnh trên đường đi đó bằng lượng luồng nhỏ nhất vừa tìm được.
7.  Lặp lại bước 2 đến bước 6 cho đến khi không còn đường tăng nào nữa trong mạng con.

**Tìm lát cắt cực tiểu**

Sau khi đã tìm được luồng cực đại, ta có thể tính được lát cắt cực tiểu bằng cách tìm các cạnh nối giữa các đỉnh thuộc phần đồ thị chứa đỉnh nguồn và phần đồ thị chứa đỉnh đích. Lát cắt cực tiểu chính là tổng trọng số của các cạnh nối các đỉnh này. cụ thể như sau:

1.  Tạo đồ thị phụ của đồ thị ban đầu: loại bỏ tất cả các cạnh không thuộc đồ thị cực đại.
2.  Sử dụng BFS để tìm lát cắt trên đồ thị phụ: bắt đầu từ đỉnh nguồn, duyệt đồ thị theo cách BFS, tìm tất cả các đỉnh có thể đến được từ đỉnh nguồn và đưa chúng vào tập S. Các đỉnh không thuộc tập S sẽ thuộc tập T.
3.  Lát cắt cực tiểu là tập các cạnh bắt đầu từ các đỉnh trong tập S và kết thúc tại các đỉnh trong tập T.

Lưu ý rằng đồ thị phụ chỉ bao gồm các cạnh thuộc đồ thị cực đại, do đó, nếu ta tìm được đường đi từ đỉnh nguồn đến một đỉnh bất kỳ trong đồ thị phụ, đỉnh đó sẽ nằm trong tập S. Tương tự, nếu đỉnh không thể được đến từ đỉnh nguồn, nó sẽ nằm trong tập T.

**Mã giả**

Đây là mã giả của thuật toán Dinic để tìm luồng cực đại trên đồ thị có hướng và có trọng số dương.

```
function Dinic(graph, source, sink):
    // Khởi tạo luồng ban đầu là 0
    maxFlow = 0
    
    // Vòng lặp chính của thuật toán
    while (true):
        // Khởi tạo mảng level để lưu trọng số đường đi tối thiểu từ đỉnh nguồn
        level = [-1, ..., -1]
        
        // Khởi tạo hàng đợi để lưu các đỉnh cần duyệt
        queue = []
        
        // Đưa đỉnh nguồn vào hàng đợi và gán level của nó là 0
        queue.push(source)
        level[source] = 0
        
        // Vòng lặp BFS để tìm đường tăng luồng
        while (len(queue) > 0):
            u = queue.pop(0)
            for v in graph[u]:
                if level[v] == -1 and graph[u][v] > 0:
                    level[v] = level[u] + 1
                    queue.push(v)
        
        // Nếu không còn đường tăng luồng nữa thì thoát vòng lặp
        if level[sink] == -1:
            break
        
        // Khởi tạo mảng ptr để lưu trạng thái đỉnh đã duyệt
        ptr = [0, ..., 0]
        
        // Hàm tìm đường tăng luồng
        function findPath(u, flow):
            if u == sink:
                return flow
            while ptr[u] < len(graph[u]):
                v = graph[u][ptr[u]][0]
                if level[v] == level[u] + 1 and graph[u][v] > 0:
                    delta = findPath(v, min(flow, graph[u][v]))
                    if delta > 0:
                        graph[u][v] -= delta
                        graph[v][u] += delta
                        return delta
                ptr[u] += 1
            return 0
        
        // Vòng lặp để tìm đường tăng luồng và cập nhật giá trị luồng
        while (true):
            flow = findPath(source, float("inf"))
            if flow == 0:
                break
            maxFlow += flow
    
    // Trả về luồng cực đại
    return maxFlow
```

Trong đó:

*   `graph` là danh sách kề của đồ thị
*   `source` là đỉnh nguồn
*   `sink` là đỉnh đích
*   `level` là mảng lưu trọng số đường đi tối thiểu từ đỉnh nguồn
*   `queue` là hàng đợi để lưu các đỉnh cần duyệt
*   `ptr` là mảng lưu trạng thái đỉnh đã duyệt
*   `maxFlow` là giá trị luồng cực đại

Và mã giả cho phương pháp tìm lát cắt cực tiểu

```
function min_cut(graph, source, sink):
    // Tạo đồ thị phụ bằng cách loại bỏ các cạnh không thuộc đồ thị cực đại
    residual_graph = create_residual_graph(graph)

    // Khởi tạo tập S với đỉnh nguồn và tập T với tất cả các đỉnh khác trong đồ thị
    S = {source}
    T = set(graph.keys()) - S

    // Tìm các đỉnh thuộc tập S và T bằng BFS trên đồ thị phụ
    queue = [source]
    visited = {source}
    while queue:
        current = queue.pop(0)
        for neighbor in residual_graph[current]:
            if neighbor not in visited and residual_graph[current][neighbor] > 0:
                visited.add(neighbor)
                S.add(neighbor)
                queue.append(neighbor)
    T = set(graph.keys()) - S

    // Lát cắt cực tiểu là tập các cạnh bắt đầu từ các đỉnh trong tập S và kết thúc tại các đỉnh trong tập T
    min_cut_edges = []
    for vertex in S:
        for neighbor in graph[vertex]:
            if neighbor in T:
                min_cut_edges.append((vertex, neighbor))

    return min_cut_edges
```

Trong đó:

*   `graph` là đồ thị ban đầu.
*   `source` là đỉnh nguồn.
*   `sink` là đỉnh đích.
*   `create_residual_graph(graph)` là hàm tạo đồ thị phụ bằng cách loại bỏ các cạnh không thuộc đồ thị cực đại.
*   `residual_graph` là đồ thị phụ.
*   `S` là tập các đỉnh thuộc tập S.
*   `T` là tập các đỉnh thuộc tập T.
*   `queue` là hàng đợi của BFS.
*   `visited` là tập các đỉnh đã được duyệt bởi BFS.
*   `min_cut_edges` là danh sách các cạnh thuộc lát cắt cực tiểu.

Lưu ý rằng mã giả này giả sử đồ thị được biểu diễn dưới dạng danh sách kề. Nếu đồ thị được biểu diễn bằng ma trận kề, cần sử dụng một số biến thay thế để lưu trữ thông tin về các đỉnh và cạnh.

**create_residual_graph(graph)**

```
function create_residual_graph(graph):
    residual_graph = {}
    for u in graph:
        residual_graph[u] = {}
        for v in graph[u]:
            residual_graph[u][v] = graph[u][v]
            residual_graph[v][u] = 0  # Thêm cạnh phản chiếu với trọng số 0
    return residual_graph
```

Trong đó, graph là đồ thị ban đầu được biểu diễn dưới dạng danh sách kề, residual_graph là đồ thị phụ cực đại được trả về. Hàm này sử dụng vòng lặp lồng nhau để duyệt qua các đỉnh và cạnh của đồ thị ban đầu, tạo các đỉnh và cạnh tương ứng trong đồ thị phụ. Trọng số của các cạnh trong đồ thị phụ được thiết lập ban đầu bằng giá trị của các cạnh trong đồ thị ban đầu, và các cạnh phản chiếu được thêm vào với trọng số ban đầu bằng 0. Cuối cùng, hàm trả về đồ thị phụ đã tạo.

## Tổng kết

Bài toán Max Flow Min Cut là bài toán quan trọng trong lý thuyết đồ thị và ứng dụng trong nhiều lĩnh vực khác nhau như mạng máy tính, giao thông vận tải, tài chính, v.v. Bài toán này có hai dạng: tìm luồng cực đại từ một đỉnh nguồn tới một đỉnh đích trên đồ thị có hướng và có trọng số dương; và tìm lát cắt cực tiểu trên đồ thị đó.

Để giải quyết bài toán này, có nhiều thuật toán được đề xuất, trong đó thuật toán Ford-Fulkerson là thuật toán cơ bản nhất. Tuy nhiên, vì có thể dẫn đến việc lặp vô hạn, nên các thuật toán tối ưu hơn như Edmonds-Karp và Dinic đã được phát triển.

Việc giải quyết bài toán luồng cực đại trên đồ thị có trọng số âm là một vấn đề khó khăn và phức tạp, và đòi hỏi các phương pháp đặc biệt để xử lý. Thông thường, trong thực tế, các đồ thị được sử dụng để giải quyết các vấn đề thực tế thường không có trọng số âm, vì vậy việc sử dụng các thuật toán như Ford-Fulkerson, Edmonds-Karp hoặc Dinic vẫn là lựa chọn tốt cho việc giải quyết bài toán luồng cực đại.

Bài toán Max Flow Min Cut không chỉ giúp tìm ra luồng cực đại hoặc lát cắt cực tiểu trên đồ thị mà còn có nhiều ứng dụng khác như tối ưu hóa hoạt động mạng máy tính, cân bằng tài nguyên, tối ưu hóa vận tải, v.v. Bài toán còn là nền tảng cho nhiều bài toán tối ưu khác trên đồ thị.

Vì vậy, bài toán Max Flow Min Cut không chỉ có ý nghĩa lý thuyết mà còn mang lại giá trị ứng dụng to lớn, đóng góp tích cực vào sự phát triển của nhiều lĩnh vực và công nghệ.
