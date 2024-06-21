**1. Priority Queue**:
Priority Queue adalah struktur data abstrak yang mirip dengan queue atau antrian, tetapi dengan setiap elemen memiliki "prioritas." Dalam priority queue, elemen dengan prioritas tertinggi akan diproses pertama, bukan elemen yang pertama kali masuk. Elemen-elemen di dalam priority queue dapat dimasukkan dalam urutan acak, tetapi ketika diambil, elemen dengan prioritas tertinggi akan selalu diambil terlebih dahulu.

**Jenis-jenis Priority Queue**:
1. **Max-Priority Queue**: Di mana elemen dengan nilai tertinggi memiliki prioritas tertinggi.
2. **Min-Priority Queue**: Di mana elemen dengan nilai terendah memiliki prioritas tertinggi.

**Heaps**:
Heap adalah implementasi umum dari priority queue. Heap adalah struktur data berbentuk pohon yang mematuhi properti heap, yang berbeda antara Min-Heap dan Max-Heap:

1. **Max-Heap**: Setiap node memiliki nilai yang lebih besar atau sama dengan nilai dari anak-anaknya. Dengan demikian, elemen terbesar berada di root.
2. **Min-Heap**: Setiap node memiliki nilai yang lebih kecil atau sama dengan nilai dari anak-anaknya. Dengan demikian, elemen terkecil berada di root.

**Ciri-ciri Heap**:
- **Complete Binary Tree**: Heap adalah pohon biner lengkap, yang berarti semua level kecuali mungkin yang terakhir diisi sepenuhnya, dan semua node pada level terakhir berada di posisi paling kiri.
- **Heap Property**: Dalam Max-Heap, nilai setiap node lebih besar atau sama dengan nilai anak-anaknya. Dalam Min-Heap, nilai setiap node lebih kecil atau sama dengan nilai anak-anaknya.

**Operasi-operasi pada Heap**:
1. **Insertion**: Menambahkan elemen baru ke heap, kemudian menyesuaikan heap dengan `shiftUp` untuk mempertahankan properti heap.
2. **Deletion**: Menghapus elemen dari heap, biasanya root (elemen tertinggi), kemudian menyesuaikan heap dengan `shiftDown`.
3. **Heapify**: Proses menyesuaikan seluruh array menjadi heap.
4. **Extract-Max/Min**: Mengambil dan menghapus elemen maksimum (dalam Max-Heap) atau elemen minimum (dalam Min-Heap) dari heap.

**Aplikasi Priority Queue dan Heaps**:
- **Scheduling**: Mengatur pekerjaan atau tugas berdasarkan prioritas.
- **Dijkstra's Algorithm**: Untuk menemukan jalur terpendek dalam graf.
- **Huffman Coding**: Untuk pengkodean data dalam algoritma kompresi.
- **Heapsort**: Algoritma pengurutan yang efisien berdasarkan heap.

Dengan memahami dasar-dasar priority queue dan heaps, kita dapat memanfaatkan struktur data ini untuk mengoptimalkan berbagai operasi yang memerlukan penanganan elemen berdasarkan prioritas.

## Contoh Program

```cpp
#include <iostream>
#include <algorithm>

int H[50];
int heapSize = -1;

int parent(int i) {
    return (i - 1) / 2;
}

int leftChild(int i) {
    return ((2 * i) + 1);
}

int rightChild(int i) {
    return ((2 * i) + 2);
}

void shiftUp(int i) {
    while (i > 0 && H[parent(i)] < H[i]) {
        std::swap(H[parent(i)], H[i]);
        i =parent(i);
    }
}

void shiftDown(int i) {
    int maxIndex = i;
    int l = leftChild(i);
    if (l <= heapSize && H[l] > H[maxIndex]) {
        maxIndex = l;
    }
    int r = rightChild(i);
    if (r <= heapSize && H[r] > H[maxIndex]) {
        maxIndex = r;
    }
    if (i != maxIndex) {
        std::swap(H[i], H[maxIndex]);
        shiftDown(maxIndex);
    }
}

void insert(int p) {
    heapSize = heapSize + 1;
    H[heapSize] = p;
    shiftUp(heapSize);
}

int extractMax() {
    int result = H[0];
    H[0] = H[heapSize];
    heapSize = heapSize -1;
    shiftDown(0);
    return result;
}

void changePriority(int i, int p) {
    int oldp = H[i];
    H[i] = p;
    if (p > oldp) {
        shiftUp(i);
    } else {
        shiftDown(i);
    }
}

int getMax() {
    return H[0];
}

void remove(int i) {
    H[i] = getMax() + 1;
    shiftUp(i);
    extractMax();
}

int main() {
    insert(45);
    insert(20);
    insert(14);
    insert(12);
    insert(31);
    insert(7);
    insert(11);
    insert(13);
    insert(7);

    std::cout << "Priority Queue : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " " ;
    }
    std::cout << "\n";

    std:: cout << "Node with maximum priority :" << extractMax() << "\n";

    std::cout << "Priority queue after extracting maximum : ";
    for (int i = 0;i <= heapSize; ++ i) {
        std::cout << H[i] << " ";
    }
    std::cout << "\n";

    changePriority(2, 49);
    std::cout << "Priority queue after priority change : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    std::cout << "\n";

    remove(3);
    std::cout << "Priority queue after removing the element : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    return 0;
}
```

**2. Hash Table**
## Dasar Teori

Hash table adalah struktur data yang menggunakan array dan fungsi hash untuk memetakan kunci ke nilai dengan efisien. Fungsi hash mengubah kunci menjadi indeks array, memungkinkan operasi pencarian, penyisipan, dan penghapusan dilakukan dengan cepat.

### Poin Penting:
1. **Fungsi Hash**: Mengubah kunci menjadi indeks dalam array.
2. **Tabrakan (Collision)**: Terjadi ketika dua kunci berbeda di-hash ke indeks yang sama.
   - **Penanganan Tabrakan**:
     - **Chaining**: Setiap elemen array adalah daftar yang menyimpan elemen yang di-hash ke indeks tersebut.
     - **Open Addressing**: Mencari slot kosong berikutnya dalam array.
3. **Kompleksitas Waktu**:
   - **Rata-rata**: O(1) untuk penyisipan, pencarian, dan penghapusan.
   - **Terburuk**: O(n) jika banyak tabrakan.
4. **Karakteristik Fungsi Hash yang Baik**:
   - Deterministik, distribusi seragam, dan cepat dihitung.

### Penggunaan:
- **Database Indexing**: Mempercepat pencarian data.
- **Caching**: Menyimpan data yang sering diakses.
- **Penghitung Frekuensi**: Menghitung kemunculan elemen dalam dataset besar.

Hash table digunakan karena efisiensinya dalam mengakses dan mengelola data secara cepat.

**Contoh Program**
```cpp
#include <iostream>
using namespace std;
const int MAX_SIZE = 10;

// Fungsi hash sederhana
int hash_func(int key) {
    return key % MAX_SIZE;
}

// Struktur data untuk setiap node
struct Node {
    int key;
    int value;
    Node* next;
    Node(int key, int value) : key(key), value(value), next(nullptr) {}
};

// Class hash table
class HashTable {
private:
    Node** table;
public:
    HashTable() {
        table = new Node*[MAX_SIZE]();
    }
    ~HashTable() {
        for (int i = 0; i < MAX_SIZE; i++) {
            Node* current = table[i];
            while (current != nullptr) {
                Node* temp = current;
                current = current->next;
                delete temp;
            }
        }
        delete[] table;
    }

    // Insertion
    void insert(int key, int value) {
        int index = hash_func(key);
        Node* current = table[index];
        while (current != nullptr) {
            if (current->key == key) {
                current->value = value;
                return;
            }
            current = current->next;
        }
        Node* node = new Node(key, value);
        node->next = table[index];
        table[index] = node;
    }

    // Searching
    int get(int key) {
        int index = hash_func(key);
        Node* current = table[index];
        while (current != nullptr) {
            if (current->key == key) {
                return current->value;
            }
            current = current->next;
        }
        return -1;
    }

    // Deletion
    void remove(int key) {
        int index = hash_func(key);
        Node* current = table[index];
        Node* prev = nullptr;
        while (current != nullptr) {
            if (current->key == key) {
                if (prev == nullptr) {
                    table[index] = current->next;
                } else {
                    prev->next = current->next;
                }
                delete current;
                return;
            }
            prev = current;
            current = current->next;
        }
    }

    // Traversal
    void traverse() {
        for (int i = 0; i < MAX_SIZE; i++) {
            Node* current = table[i];
            while (current != nullptr) {
                cout << current->key << ": " << current->value << endl;
                current = current->next;
            }
        }
    }
};

int main() {
    HashTable ht;
    // Insertion
    ht.insert(1, 10);
    ht.insert(2, 20);
    ht.insert(3, 30);

    // Searching
    cout << "Get key 1: " << ht.get(1) << endl;
    cout << "Get key 4: " << ht.get(4) << endl;
   
    // Deletion
    ht.remove(4);
   
    // Traversal
    ht.traverse();
   
    return 0;
}
```

**3. Rekrusif**

## Dasar Teori

Rekursif adalah teknik pemrograman di mana sebuah fungsi memanggil dirinya sendiri untuk menyelesaikan suatu masalah. Teknik ini sangat berguna dalam algoritma dan struktur data untuk menyederhanakan masalah kompleks menjadi sub-masalah yang lebih sederhana. Fungsi rekursif memiliki dua bagian utama: kasus dasar (base case) dan kasus rekursif (recursive case).

**Kasus Dasar**: Merupakan kondisi di mana fungsi berhenti memanggil dirinya sendiri. Tanpa kasus dasar, fungsi akan terus memanggil dirinya sendiri tanpa henti, menyebabkan infinite recursion dan akhirnya stack overflow.

**Kasus Rekursif**: Bagian di mana fungsi memanggil dirinya sendiri dengan argumen yang dimodifikasi, mendekati kasus dasar dengan setiap panggilan rekursif.
Contoh Kasus Penggunaan Rekursif:

- **Faktorial**: Menghitung hasil kali dari semua bilangan bulat positif hingga bilangan tertentu.
Fibonacci: Menghitung bilangan Fibonacci ke-n.
- **Pencarian dan Penelusuran dalam Struktur Data**: Seperti pohon biner dan graf.
- **Algoritma Pembagian dan Penaklukan (Divide and Conquer)**: Seperti quicksort dan mergesort.

## Contoh Programa

```cpp
#include <iostream>
/// Rekursif Langsung
using namespace std;

void countdown(int n) {
    if (n == 0) {
        return;
    }

    cout << n << " ";
    countdown(n-1);
}

int main() {
    cout << "Rekursi Langsung: ";
    countdown(5);
    cout << endl;
    return 0;
}
```

## GUIDED 2
```cpp
#include <iostream>
/// Rekursif Tidak Langsung
using namespace std;

void functionB(int n);

void functionA(int n) {
    if (n > 0) {
        cout << n << " ";
        functionB(n - 1);
    }
}

void functionB(int n) {
    if (n > 0) {
        cout << n << " ";
        functionA(n / 2);
    }
}
 
int main() {
    int num = 5;
    cout << "Rekursif Tidak Langsung: ";
    functionA(num);
    return 0;
}
```

**4. Graph & Tree**

## Dasar Teori

1. *Graph* adalah struktur data yang terdiri dari simpul (vertices) dan tepi (edges) yang menghubungkan simpul-simpul tersebut. Graph digunakan untuk merepresentasikan hubungan antar objek, seperti jaringan komputer, rute transportasi, dan hubungan sosial. Ada dua jenis graph utama: *graph berarah* (directed graph) dan *graph tak berarah* (undirected graph). Algoritma umum yang digunakan pada graph meliputi *Breadth-First Search (BFS), **Depth-First Search (DFS), algoritma **Dijkstra* untuk menemukan jalur terpendek, dan *algoritma Kruskal* serta *algoritma Prim* untuk mencari minimum spanning tree.

2. *Tree* adalah struktur data hierarkis yang terdiri dari simpul dengan satu simpul akar (root) dan simpul-simpul anak (children) yang terhubung. Setiap simpul dalam tree memiliki tepat satu induk kecuali simpul akar yang tidak memiliki induk. Contoh spesifik dari tree adalah *binary tree, **binary search tree (BST), dan **heap*. Tree digunakan dalam berbagai aplikasi seperti database (untuk struktur B-tree), compiler (untuk pohon sintaksis), dan algoritma Huffman untuk kompresi data.

### Implementasi dan Penggunaan:
- *Breadth-First Search (BFS)* digunakan untuk traversing atau searching struktur data tree atau graph. BFS memanfaatkan antrian (queue) untuk melacak simpul yang harus dieksplorasi, memastikan setiap simpul pada level tertentu diakses sebelum berpindah ke level berikutnya
- *Graph Neural Networks (GNNs)* adalah penerapan terbaru yang menggabungkan pembelajaran mesin dengan graph untuk melakukan tugas-tugas seperti klasifikasi node, prediksi link, dan klastering graf, yang relevan dalam bidang seperti biologi komputasi dan jaringan sosial 

## Contoh Pemograman

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

string simpul[7] = {
    "Ciamis", "Bandung", "Tasikmalaya", "Cianjur", "Purwokerto", "Yogyakarta"
};

int busur[7][7] = {
    {0, 7, 8, 0, 0, 0, 0},
    {0, 0, 5, 0, 0, 15, 0},
    {0, 6, 0, 0, 5, 0, 0},
    {0, 5, 0, 0, 2, 4, 0},
    {23, 0, 0, 10, 0, 0, 8},
    {0, 0, 0, 0, 7, 0, 3},
    {0, 0, 0, 0, 9, 4, 0},
};

void tampilGraph() {
    for (int baris = 0; baris < 7; baris ++) {
        cout << " " << setiosflags(ios::left) << setw(15) << simpul[baris] << ":";
        for (int kolom = 0; kolom < 7; kolom ++) {
            if (busur [baris][kolom] != 0) {
                cout << " " << simpul[kolom] << "(" << busur[baris][kolom] << ")";
            }
        }
        cout << endl;
    }
}

int main() {
    tampilGraph();
    return 0;
}
```

## GUIDED 2
```cpp
#include <iostream>
using namespace std;

struct TNode {
    int data;
    TNode *left;
    TNode *right;

    //constuctor
    TNode(int value) {
        data = value;
        left = NULL;
        right = NULL;
    }
};

void preOrder (TNode *node) {
    if (node != NULL) {
        cout << node->data << " ";
        preOrder(node->left);
        preOrder(node->right);
    }
}

void inOrder (TNode *node) {
    if (node != NULL) {
        inOrder(node->left);
        cout << node->data << " ";
        inOrder(node->right);
    }
}

void postOrder (TNode *node) {
    if (node != NULL) {
        postOrder(node->left);
        postOrder(node->right);
        cout << node->data << " ";
    }
}

int main() {
    TNode*zero = new TNode(0);
    TNode*one = new TNode(1);
    TNode*five = new TNode(5);
    TNode*seven = new TNode(7);
    TNode*eight = new TNode(8);
    TNode*nine = new TNode(9);

    seven->left = one;

    seven->right = nine;

    one->left = zero;

    one->right = five;

    nine->left = eight;

    preOrder(seven);
    cout << endl;

    inOrder(seven);
    cout << endl;

    postOrder(seven);
    cout << endl;

    return 0;
}
```