# <h1 align="center">Evaluasi Penilaian Tengah Semester Struktur Data</h1>
<p align="center">Brian Nugraha Wiyono</p>

## SubCPMK 2

## SOAL
1.	Terdapat tiga algoritma sorting yang umum digunakan yakni, Bubble Sort, Selection Sort, dan Merge Sort. Berikan penjelasan alur dari masing-masing algoritma tersebut, dan jelaskan runtime dari best case dan worst case masing-masing algoritma! (35 Poin)

2.	Buatlah fungsi dari salah satu algoritma sorting pada soal nomor 1, dan berikan penjelasan pada program tersebut (35 poin)

## JAWABAN
### 1. Algoritma Sorting

#### a. Bubble Sort:
- **Penjelasan Alur**:
  1. Dimulai dari indeks pertama, bandingkan setiap elemen dengan elemen berikutnya.
  2. Jika elemen saat ini lebih besar dari elemen berikutnya, tukar posisinya.
  3. Ulangi langkah 1-2 hingga tidak ada lagi pertukaran yang dilakukan dalam satu iterasi.
  4. Setelah iterasi selesai, elemen terbesar akan berada di posisi paling kanan.
  5. Ulangi langkah 1-4 hingga seluruh array terurut.

- **Runtime**:
  - **Best Case**: O(n) (ketika array sudah terurut dan tidak ada pertukaran yang dilakukan)
  - **Worst Case**: O(n^2) (ketika array terurut secara terbalik, sehingga memerlukan banyak pertukaran)

#### b. Selection Sort:
- **Penjelasan Alur**:
  1. Bagi array menjadi dua bagian: bagian terurut dan bagian belum terurut.
  2. Pada setiap iterasi, pilih elemen terkecil dari bagian belum terurut dan tukar dengan elemen paling kiri dari bagian belum terurut.
  3. Perluas bagian terurut dengan memindahkan batasnya satu posisi ke kanan.
  4. Ulangi langkah 2-3 hingga seluruh array terurut.

- **Runtime**:
  - **Best Case**: O(n^2) (karena jumlah perbandingan dan pertukaran tetap sama, tidak peduli apakah array sudah terurut atau tidak)
  - **Worst Case**: O(n^2) (sama seperti best case karena setiap elemen harus diperiksa dan ditukar)

#### c. Merge Sort:
- **Penjelasan Alur**:
  1. Bagi array menjadi dua bagian sama besar.
  2. Urutkan kedua bagian secara rekursif dengan menggunakan Merge Sort.
  3. Gabungkan dua bagian yang telah terurut menjadi satu bagian utuh yang terurut.

- **Runtime**:
  - **Best Case**: O(n log n) (karena pada setiap level rekursif, array dibagi menjadi dua bagian yang sama besar dan hanya dilakukan satu kali penggabungan)
  - **Worst Case**: O(n log n) (sama seperti best case, karena jumlah operasi pada setiap level tetap)

### 2. Implementasi Fungsi Selection Sort:

Berikut adalah contoh implementasi fungsi Selection Sort dalam C++ beserta penjelasan singkatnya:

```cpp
#include <iostream>
#include <vector>

// Fungsi Selection Sort
void selectionSort(std::vector<int> &arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; ++i) {
        int minIndex = i;
        for (int j = i + 1; j < n; ++j) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        // Tukar elemen terkecil dengan elemen pertama pada bagian belum terurut
        std::swap(arr[i], arr[minIndex]);
    }
}

int main() {
    std::vector<int> arr = {64, 25, 12, 22, 11};
    selectionSort(arr);
    std::cout << "Array setelah diurutkan: ";
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    return 0;
}
```

- **Penjelasan Program**: Program di atas mengimplementasikan fungsi `selectionSort` untuk mengurutkan array menggunakan algoritma Selection Sort. Pada setiap iterasi, algoritma ini mencari elemen terkecil dari bagian belum terurut dan menukar posisinya dengan elemen paling kiri dari bagian belum terurut. Selanjutnya, bagian terurut diperluas dengan memindahkan batasnya satu posisi ke kanan. Program kemudian mencetak array setelah diurutkan.

## SubCPMK 3
## Soal
1.	Terdapat dua algoritma searching yang umum digunakan yakni, Binary Search dan Linear Search. Berikan penjelasan alur dari masing-masing algoritma tersebut, dan jelaskan runtime dari best case dan worst case masing-masing algoritma! (35 Poin)
2.	Buatlah fungsi dari salah satu algoritma searching pada soal nomor 1, dan berikan penjelasan pada program tersebut (35 Poin)

## Jawaban

### 1. Algoritma Searching

#### a. Binary Search:
- **Penjelasan Alur**: 
  1. Diawali dengan sebuah array terurut.
  2. Tentukan elemen tengah dari array.
  3. Bandingkan elemen tengah dengan nilai yang dicari.
  4. Jika nilai sama, kembalikan indeks tengah.
  5. Jika nilai lebih besar, cari di setengah kanan array.
  6. Jika nilai lebih kecil, cari di setengah kiri array.
  7. Ulangi langkah 2-6 hingga elemen ditemukan atau array habis.

- **Runtime**:
  - **Best Case**: O(1) (ketika nilai yang dicari adalah elemen tengah array)
  - **Worst Case**: O(log n) (ketika nilai yang dicari tidak ada dalam array atau berada di ujung array)

#### b. Linear Search:
- **Penjelasan Alur**:
  1. Diawali dengan sebuah array.
  2. Mulai dari indeks pertama, bandingkan setiap elemen dengan nilai yang dicari.
  3. Jika nilai ditemukan, kembalikan indeks elemen tersebut.
  4. Jika nilai tidak ditemukan, lanjut ke elemen berikutnya.
  5. Ulangi langkah 2-4 hingga elemen ditemukan atau array habis.

- **Runtime**:
  - **Best Case**: O(1) (ketika nilai yang dicari adalah elemen pertama array)
  - **Worst Case**: O(n) (ketika nilai yang dicari tidak ada dalam array atau berada di posisi terakhir array)

### 2. Implementasi Fungsi Binary Search:

Berikut adalah contoh implementasi fungsi Binary Search dalam C++ beserta penjelasan singkatnya:

```cpp
#include <iostream>
#include <vector>

// Fungsi Binary Search
int binarySearch(std::vector<int> arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        // Jika nilai yang dicari adalah elemen tengah
        if (arr[mid] == target) {
            return mid;
        }

        // Jika nilai yang dicari berada di setengah kiri array
        if (arr[mid] < target) {
            left = mid + 1;
        } 
        // Jika nilai yang dicari berada di setengah kanan array
        else {
            right = mid - 1;
        }
    }

    // Jika nilai tidak ditemukan
    return -1;
}

int main() {
    std::vector<int> arr = {2, 5, 8, 12, 16, 23, 38, 56, 72, 91};
    int target = 23;
    int result = binarySearch(arr, target);
    if (result != -1) {
        std::cout << "Elemen ditemukan pada indeks: " << result << std::endl;
    } else {
        std::cout << "Elemen tidak ditemukan dalam array." << std::endl;
    }
    return 0;
}
```

- **Penjelasan Program**: Program di atas mengimplementasikan fungsi `binarySearch` untuk mencari nilai target dalam array yang telah diurutkan. Fungsi ini menggunakan algoritma Binary Search. Array diurutkan terlebih dahulu untuk memastikan keberhasilan pencarian dengan algoritma ini. Jika nilai ditemukan, program akan mencetak indeks elemen tersebut; jika tidak, program akan mencetak pesan bahwa elemen tidak ditemukan.

## SubCPMK 4
## Soal
1.	Buatlah sebuah fungsi program untuk menghilangkan duplikasi data pada unsorted linked list (single atau double atau circular) (40 Poin)
2.	Buatlah sebuah program untuk mengecek apakah linked list adalah sebuah palindrom! (50 Poin)

## Jawaban
1. 
```cpp
#include <iostream>
#include <unordered_set>

struct Node {
    int data;
    Node* next;
    Node(int value) : data(value), next(nullptr) {}
};

void removeDuplicates(Node* head) {
    if (head == nullptr) return;

    std::unordered_set<int> seen;
    Node* current = head;
    Node* prev = nullptr;

    while (current != nullptr) {
        if (seen.find(current->data) != seen.end()) {
            // Data sudah ada sebelumnya, hapus node
            prev->next = current->next;
            delete current;
            current = prev->next;
        } else {
            // Data belum pernah muncul sebelumnya, tambahkan ke set dan lanjutkan
            seen.insert(current->data);
            prev = current;
            current = current->next;
        }
    }
}

// Fungsi untuk mencetak linked list
void printList(Node* node) {
    while (node != nullptr) {
        std::cout << node->data << " ";
        node = node->next;
    }
    std::cout << std::endl;
}

int main() {
    Node* head = new Node(10);
    head->next = new Node(12);
    head->next->next = new Node(11);
    head->next->next->next = new Node(11);
    head->next->next->next->next = new Node(12);
    head->next->next->next->next->next = new Node(11);
    head->next->next->next->next->next->next = new Node(10);

    std::cout << "Linked list sebelum dihapus duplikasinya: \n";
    printList(head);

    removeDuplicates(head);

    std::cout << "Linked list setelah dihapus duplikasinya: \n";
    printList(head);

    return 0;
}
```
2. 
```cpp
#include <iostream>
#include <stack>

struct Node {
    int data;
    Node* next;
    Node(int value) : data(value), next(nullptr) {}
};

// Fungsi untuk mengecek apakah linked list adalah palindrom
bool isPalindrome(Node* head) {
    if (head == nullptr || head->next == nullptr) {
        return true; // Linked list kosong atau hanya memiliki satu elemen, dianggap palindrom
    }

    Node* slow = head;
    Node* fast = head;
    std::stack<int> firstHalf;

    // Temukan tengah linked list dan tambahkan setengah bagian pertama ke stack
    while (fast != nullptr && fast->next != nullptr) {
        firstHalf.push(slow->data);
        slow = slow->next;
        fast = fast->next->next;
    }

    // Jika linked list memiliki jumlah elemen ganjil, lewati elemen tengah
    if (fast != nullptr) {
        slow = slow->next;
    }

    // Bandingkan setengah bagian pertama dengan setengah bagian kedua yang telah dibalik
    while (slow != nullptr) {
        int top = firstHalf.top();
        firstHalf.pop();
        if (top != slow->data) {
            return false; // Tidak palindrom
        }
        slow = slow->next;
    }

    return true; // Palindrom
}

// Fungsi untuk menambahkan node baru ke linked list
void push(Node** head_ref, int new_data) {
    Node* new_node = new Node(new_data);
    new_node->next = (*head_ref);
    (*head_ref) = new_node;
}

// Fungsi untuk mencetak linked list
void printList(Node* node) {
    while (node != nullptr) {
        std::cout << node->data << " ";
        node = node->next;
    }
    std::cout << std::endl;
}

int main() {
    Node* head = nullptr;
    push(&head, 1);
    push(&head, 2);
    push(&head, 3);
    push(&head, 2);
    push(&head, 1);

    std::cout << "Linked list: \n";
    printList(head);

    if (isPalindrome(head)) {
        std::cout << "Linked list adalah palindrom.\n";
    } else {
        std::cout << "Linked list bukan palindrom.\n";
    }

    return 0;
}
```

## SubCPMK 5
## Soal
1.	Tulislah sebuah program dari operasi stack seperti pop, push, isEmpty, isFull, dll(min 5)! (60 Poin)

## Jawaban
```cpp
#include <iostream>

#define MAX_SIZE 100

class Stack {
private:
    int top;
    int stack[MAX_SIZE];

public:
    Stack() {
        top = -1;
    }

    // Menambahkan elemen ke stack
    void push(int value) {
        if (top >= MAX_SIZE - 1) {
            std::cout << "Stack penuh, tidak bisa menambahkan elemen." << std::endl;
            return;
        }
        stack[++top] = value;
        std::cout << "Elemen " << value << " ditambahkan ke stack." << std::endl;
    }

    // Menghapus elemen dari stack
    void pop() {
        if (top < 0) {
            std::cout << "Stack kosong, tidak ada elemen yang bisa dihapus." << std::endl;
            return;
        }
        int value = stack[top--];
        std::cout << "Elemen " << value << " dihapus dari stack." << std::endl;
    }

    // Mengembalikan elemen paling atas dari stack tanpa menghapusnya
    int peek() {
        if (top < 0) {
            std::cout << "Stack kosong." << std::endl;
            return -1;
        }
        return stack[top];
    }

    // Mengecek apakah stack kosong
    bool isEmpty() {
        return top < 0;
    }

    // Mengecek apakah stack penuh
    bool isFull() {
        return top >= MAX_SIZE - 1;
    }

    // Mengembalikan jumlah elemen dalam stack
    int size() {
        return top + 1;
    }
};

int main() {
    Stack stack;

    std::cout << "Stack kosong? " << (stack.isEmpty() ? "Ya" : "Tidak") << std::endl;

    stack.push(1);
    stack.push(2);
    stack.push(3);
    stack.push(4);
    stack.push(5);

    std::cout << "Stack penuh? " << (stack.isFull() ? "Ya" : "Tidak") << std::endl;

    std::cout << "Elemen paling atas: " << stack.peek() << std::endl;

    stack.pop();
    stack.pop();

    std::cout << "Jumlah elemen dalam stack: " << stack.size() << std::endl;

    std::cout << "Stack kosong? " << (stack.isEmpty() ? "Ya" : "Tidak") << std::endl;

    return 0;
}
```

## SubCPMK 6
## Soal
1.	Tulislah sebuah program dari operasi queue seperti enqueue/add, dequeue/remove, isEmpty, isFull, dll(min 5)! (60 Poin)

## Jawaban
```cpp
#include <iostream>

#define MAX_SIZE 100

class Queue {
private:
    int front, rear, size;
    int queue[MAX_SIZE];

public:
    Queue() {
        front = rear = -1;
        size = 0;
    }

    // Menambahkan elemen ke queue
    void enqueue(int value) {
        if (isFull()) {
            std::cout << "Queue penuh, tidak bisa menambahkan elemen." << std::endl;
            return;
        }
        if (isEmpty()) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % MAX_SIZE;
        }
        queue[rear] = value;
        size++;
        std::cout << "Elemen " << value << " ditambahkan ke queue." << std::endl;
    }

    // Menghapus elemen dari queue
    void dequeue() {
        if (isEmpty()) {
            std::cout << "Queue kosong, tidak ada elemen yang bisa dihapus." << std::endl;
            return;
        }
        int value = queue[front];
        if (front == rear) {
            front = rear = -1;
        } else {
            front = (front + 1) % MAX_SIZE;
        }
        size--;
        std::cout << "Elemen " << value << " dihapus dari queue." << std::endl;
    }

    // Mengembalikan elemen paling depan dari queue tanpa menghapusnya
    int peek() {
        if (isEmpty()) {
            std::cout << "Queue kosong." << std::endl;
            return -1;
        }
        return queue[front];
    }

    // Mengecek apakah queue kosong
    bool isEmpty() {
        return size == 0;
    }

    // Mengecek apakah queue penuh
    bool isFull() {
        return size == MAX_SIZE;
    }

    // Mengembalikan jumlah elemen dalam queue
    int getSize() {
        return size;
    }
};

int main() {
    Queue queue;

    std::cout << "Queue kosong? " << (queue.isEmpty() ? "Ya" : "Tidak") << std::endl;

    queue.enqueue(1);
    queue.enqueue(2);
    queue.enqueue(3);
    queue.enqueue(4);
    queue.enqueue(5);

    std::cout << "Queue penuh? " << (queue.isFull() ? "Ya" : "Tidak") << std::endl;

    std::cout << "Elemen paling depan: " << queue.peek() << std::endl;

    queue.dequeue();
    queue.dequeue();

    std::cout << "Jumlah elemen dalam queue: " << queue.getSize() << std::endl;

    std::cout << "Queue kosong? " << (queue.isEmpty() ? "Ya" : "Tidak") << std::endl;

    return 0;
}
```