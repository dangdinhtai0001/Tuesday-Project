## Giới thiệu bài toán

Bài toán luồng cực đại và lát cắt cực tiểu là hai bài toán quan trọng trong lý thuyết đồ thị. Bài toán luồng cực đại đặt ra câu hỏi tìm cách truyền dữ liệu từ nguồn đến đích sao cho lượng dữ liệu truyền được là lớn nhất, trong khi đó bài toán lát cắt cực tiểu tìm cách cắt đồ thị thành hai phần sao cho tổng trọng số của các cạnh bị cắt là nhỏ nhất.

Cả hai bài toán này đều được ứng dụng rộng rãi trong thực tiễn, ví dụ như trong mạng lưới giao thông, mạng máy tính hay trong kế toán tài chính. Giải quyết thành công các bài toán này không chỉ giúp tối ưu hóa hoạt động mà còn giúp đưa ra những quyết định đúng đắn và chính xác.

Để giải quyết bài toán luồng cực đại và lát cắt cực tiểu, các nhà nghiên cứu đã đưa ra nhiều phương pháp khác nhau, nhưng phương pháp cơ bản nhất là phương pháp Ford-Fulkerson. Đây là phương pháp tham lam (greedy) cập nhật luồng trên một đường tăng trọng số (augmenting path) trong mạng, đến khi không còn đường tăng trọng số nào nữa.

Ngoài phương pháp Ford-Fulkerson, còn có các phương pháp giải khác như:

- `Edmonds-Karp`: Là một biến thể của Ford-Fulkerson, sử dụng thuật toán tìm đường ngắn nhất để tăng cường luồng.
- `Dinic's Algorithm`: Đây là một phương pháp tăng cường luồng hiệu quả hơn so với Ford-Fulkerson và Edmonds-Karp b- ằng cách sử dụng phân lớp mạng (layered network) để tìm đường tăng trọng số.
- `Push-Relabel Algorithm`: Có thể xem là một phương pháp cải tiến của Ford-Fulkerson, sử dụng hai hoạt động đẩy (push) và nạp (relabel) để tăng cường luồng, giúp tăng tốc độ tính toán.
- `Capacity Scaling`: Là một phương pháp tham lam, tối ưu hóa việc tăng cường luồng bằng cách tăng giá trị luồng theo từng cấp số nhân của 2, cho đến khi đạt được luồng tối đa.

Ứng dụng của bài toán Max Flow Min Cut
- Mô hình hóa dòng chảy trong một mạng lưới vận tải
- Mô hình hóa lưu lượng mạng
- Ứng dụng trong bài toán tối ưu hóa

## Giải quyết bài toán

### Một sô khái niệm

- **Đồ thị (Graph)**: Là tập hợp các đỉnh (node) và cạnh (edge) nối các đỉnh với nhau
- **Luồng (Flow)**: Là lượng dữ liệu được truyền từ nguồn đến đích thông qua đồ thị. Giá trị của luồng được đo bằng trọng số (weight) của các cạnh.
- **Lát cắt (Cut)**: Là tập hợp các cạnh được chọn để cắt đồ thị thành hai phần, một phần chứa nguồn và một phần chứa đích.
- **Luồng cực đại (Maximum flow)**: Là luồng (flow) có giá trị lớn nhất .
- **Lát cắt cực tiểu (Minimum cut)**: Là lát cắt (cut) mà tổng trọng số của các cạnh của nó nhỏ nhất.
- **Đỉnh nguồn (Source vertex)**: Là đỉnh trong đồ thị mà luồng bắt đầu từ đó.
- **Đỉnh đích (Sink vertex)**: Là đỉnh trong đồ thị mà luồng chảy tới đó.
- **Đỉnh trung gian (Intermediate vertex)**: Là đỉnh nằm giữa đỉnh nguồn và đỉnh đích trong đồ thị.
- **Cạnh có hướng (Directed edge)**: Là cạnh (edge) của đồ thị và có hướng chỉ đi từ đỉnh này đến đỉnh khác.
- **Độ dư (Residual capacity)**: Là lượng luồng còn lại có thể đi qua một cạnh sau khi một luồng đã được truyền qua cạnh đó ( Một số tài liệu sẽ gọi là giá trị thặng dư ).

### Một số thuật toán

#### Thuật toán Ford-Fulkerson

Để giải bài toán luồng cực đại và lát cắt cực tiểu, ta có thể sử dụng thuật toán `Ford-Fulkerson` hoặc thuật toán `Edmonds-Karp`. Dưới đây là mô tả sơ lược về cách thức giải quyết bài toán bằng thuật toán Ford-Fulkerson:

1.  Khởi tạo luồng ban đầu bằng 0.
    
2.  Tìm một đường đi từ đỉnh nguồn tới đỉnh đích trong đồ thị.
    
3.  Tìm luồng nhỏ nhất trên đường đi vừa tìm được.
    
4.  Tăng luồng trên các cạnh trên đường đi đó bằng lượng luồng nhỏ nhất vừa tìm được.
    
5.  Lặp lại bước 2 đến khi không còn đường đi nào từ đỉnh nguồn tới đỉnh đích trong đồ thị.
    

Sau khi đã tìm được luồng cực đại, ta có thể tính được lát cắt cực tiểu bằng cách tìm các cạnh nối giữa các đỉnh thuộc phần đồ thị chứa đỉnh nguồn và phần đồ thị chứa đỉnh đích. Lát cắt cực tiểu chính là tổng trọng số của các cạnh nối các đỉnh này.

Thuật toán Ford-Fulkerson là một thuật toán tìm kiếm theo chiều sâu (DFS) và có thể không cho kết quả chính xác trong trường hợp đồ thị có trọng số âm hoặc có chu trình âm. Trong trường hợp này, ta có thể sử dụng thuật toán Edmonds-Karp để giải quyết bài toán.

#### Thuật toán Edmonds-Karp
Thuật toán Edmonds-Karp là một thuật toán giải bài toán luồng cực đại và lát cắt cực tiểu trên đồ thị có hướng và có trọng số dương. Đây là một thuật toán tối ưu về mặt thời gian so với thuật toán Ford-Fulkerson.

Dưới đây là các bước giải quyết bài toán luồng cực đại và lát cắt cực tiểu bằng thuật toán Edmonds-Karp:

1.  Khởi tạo luồng ban đầu bằng 0.
    
2.  Tìm một đường đi từ đỉnh nguồn tới đỉnh đích trong đồ thị bằng thuật toán tìm kiếm theo chiều rộng (BFS).
    
3.  Tìm luồng nhỏ nhất trên đường đi vừa tìm được.
    
4.  Tăng luồng trên các cạnh trên đường đi đó bằng lượng luồng nhỏ nhất vừa tìm được.
    
5.  Lặp lại bước 2 và 4 cho đến khi không còn đường đi nào từ đỉnh nguồn tới đỉnh đích trong đồ thị.
    

Sau khi đã tìm được luồng cực đại, ta có thể tính được lát cắt cực tiểu bằng cách tìm các cạnh nối giữa các đỉnh thuộc phần đồ thị chứa đỉnh nguồn và phần đồ thị chứa đỉnh đích. Lát cắt cực tiểu chính là tổng trọng số của các cạnh nối các đỉnh này.

Thuật toán Edmonds-Karp đảm bảo cho kết quả chính xác cho bài toán luồng cực đại và lát cắt cực tiểu trên đồ thị có hướng và có trọng số dương. Đồng thời, nó cũng đảm bảo thời gian chạy tối ưu hơn so với thuật toán Ford-Fulkerson.

#### Thuật toán Dinic

Thuật toán Dinic là một thuật toán khác để giải bài toán luồng cực đại và lát cắt cực tiểu trên đồ thị có hướng và có trọng số dương. Thuật toán này sử dụng phương pháp xây dựng mạng tăng dần (augmenting path) để tìm luồng cực đại trên đồ thị.

Dưới đây là các bước giải quyết bài toán luồng cực đại và lát cắt cực tiểu bằng thuật toán Dinic:

1.  Khởi tạo luồng ban đầu bằng 0.
    
2.  Tạo một mạng con (residual network) trên đồ thị với trọng số còn lại trên mỗi cạnh là bằng trọng số gốc trừ đi luồng hiện tại.
    
3.  Sử dụng thuật toán tìm kiếm theo chiều rộng (BFS) để tìm một đường tăng trong mạng con.
    
4.  Nếu không tìm được đường tăng nào nữa, kết thúc thuật toán.
    
5.  Nếu tìm được đường tăng, tính luồng nhỏ nhất trên đường tăng đó.
    
6.  Tăng luồng trên các cạnh trên đường đi đó bằng lượng luồng nhỏ nhất vừa tìm được.
    
7.  Lặp lại bước 2 đến bước 6 cho đến khi không còn đường tăng nào nữa trong mạng con.
    

Sau khi đã tìm được luồng cực đại, ta có thể tính được lát cắt cực tiểu bằng cách tìm các cạnh nối giữa các đỉnh thuộc phần đồ thị chứa đỉnh nguồn và phần đồ thị chứa đỉnh đích. Lát cắt cực tiểu chính là tổng trọng số của các cạnh nối các đỉnh này.

Thuật toán Dinic đảm bảo cho kết quả chính xác cho bài toán luồng cực đại và lát cắt cực tiểu trên đồ thị có hướng và có trọng số dương. Đồng thời, nó cũng đảm bảo thời gian chạy tối ưu hơn so với thuật toán Edmonds-Karp trên một số trường hợp.

### Triển khai thuật toán

#### Thuật toán Ford-Fulkerson

Đây là mã giả của thuật toán Ford-Fulkerson để tìm luồng cực đại trên đồ thị có hướng và có trọng số dương.

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

Thuật toán Ford-Fulkerson sử dụng phương pháp tìm kiếm theo chiều rộng BFS để tìm đường tăng luồng và cập nhật giá trị luồng trên đồ thị. Quá trình lặp sẽ tiếp tục cho đến khi không còn đường tăng luồng nữa.

#### Thuật toán Dinic

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

Thuật toán Dinic sử dụng phương pháp tìm kiếm theo chiều rộng (BFS) để tìm đường tăng luồng. Sau khi tìm được đường tăng luồng, giá trị luồng của đường đó được cập nhật và cứ như vậy, thuật toán tiếp tục tìm đường tăng luồng cho đến khi không còn đường tăng luồng nữa.

Với độ phức tạp là O(V^2E) trong trường hợp tổng số đường đi tăng luồng lớn, thuật toán Dinic thường được sử dụng để giải quyết bài toán luồng cực đại trên các đồ thị có kích thước nhỏ và có cấu trúc đặc biệt, chẳng hạn như trong các ứng dụng mạng máy tính.


## Tổng kết

Bài toán Max Flow Min Cut là bài toán quan trọng trong lý thuyết đồ thị và ứng dụng trong nhiều lĩnh vực khác nhau như mạng máy tính, giao thông vận tải, tài chính, v.v. Bài toán này có hai dạng: tìm luồng cực đại từ một đỉnh nguồn tới một đỉnh đích trên đồ thị có hướng và có trọng số dương; và tìm lát cắt cực tiểu trên đồ thị đó.

Để giải quyết bài toán này, có nhiều thuật toán được đề xuất, trong đó thuật toán Ford-Fulkerson là thuật toán cơ bản nhất. Tuy nhiên, vì có thể dẫn đến việc lặp vô hạn, nên các thuật toán tối ưu hơn như Edmonds-Karp và Dinic đã được phát triển.

Tuy nhiên, bài toán Max Flow Min Cut không chỉ giúp tìm ra luồng cực đại hoặc lát cắt cực tiểu trên đồ thị mà còn có nhiều ứng dụng khác như tối ưu hóa hoạt động mạng máy tính, cân bằng tài nguyên, tối ưu hóa vận tải, v.v. Bài toán còn là nền tảng cho nhiều bài toán tối ưu khác trên đồ thị.

Vì vậy, bài toán Max Flow Min Cut không chỉ có ý nghĩa lý thuyết mà còn mang lại giá trị ứng dụng to lớn, đóng góp tích cực vào sự phát triển của nhiều lĩnh vực và công nghệ.
