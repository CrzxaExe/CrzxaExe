Doubly Linked List

# Struct
```c++
struct Node {
  *Node prev // hanya doubly list
  data
  *Node next
}

// atau jika sudah menggunakan typedef

struct Node {
  alamat prev
  data
  alamat next
}
```

# Perbedaan Singly & Doubly Linked List
- Doubly List bisa 2 arah
- Doubly List memiliki Head & Tail, Singly List hanya Head
- Jika hanya mempunyai potongan dari Doubly List, maka keseluruhan dari Doubly List bisa di dapat, Singly hanya bisa mendapatkan keseluruhan data jika mulai dari Headnya
- Penyimpanan Doubly List akan lebih besar ketimbang Singly List

# Note
Untuk mempermudah bisa tambahkan typedef
```c++
typedef  struct Node *alamat;
```

# Inisiasi
```c++
// inisiasi global data
alamat first;
alamat last; // hanya doubly list
```

# Methods
 1. alokasi / createNode

konsep: mengembalikan variable bertipe alamat baru dengan data sesuai input

```c++
alamat alokasi(int data) {// tipe data bisa bebas sesuai yg diperlukan
  alamat baru = new Node;
  baru->data = data;
  baru->prev = NULL;  // hanya doubly list
  baru->next = NULL;
  return baru;
}
```

2. insertFirst

konsep: alamat baru->next akan diisi alamat first, lalu alamat first akan ditukar dengan alamat baru, jika doubly list maka sebelum menukar alamat first maka isi first->prev dengan alamat baru

```c++
void insertFirst(alamat baru) {
  baru->next = first;
  first->prev = baru; // hanya doubly list
  first = baru;
 if(last == NULL) last = baru; // hanya doubly list
}
```

3. insertLast

konsep: sama seperti insertFirst, tetapi di bagian terakhir dari list, singly list membutuhkan pengulangan

```c++
// singly list
void insertLast(alamat baru) {
  alamat tmp = first;
  while(tmp->next != NULL) {
    tmp = tmp->next;
  }

  tmp->next = baru;
}

// doubly list
void insertLast(alamat baru) {
  baru->prev = last;
  last->next = baru;
  last = baru;
  if(first == NULL) first = baru;
}
```

4. insertAfter

konsep: menambahkan alamat baru setelah data yang di cari dengan cara mencari nilai data yg dicari dgn pengulangan

```c++
void insertAfter(int cari, alamat baru) { // forward
  alamat tmp = first;
  while(tmp->data != cari && tmp->next != NULL) {
    tmp = tmp->next;
  }

  if(tmp->next->next != NULL) {
    tmp->next->prev = baru; // hanya doubly list
    baru->next = tmp->next;
  }

  tmp->next = baru;
  baru->prev = tmp; // hanya doubly list
}

void insertAfter(int cari, alamat baru) { // backward - hanya doubly list
  alamat tmp = last;
  while(tmp->data != cari && tmp->prev != NULL) {
    tmp = tmp->prev;
  }

  if(tmp->next->next != NULL) {
    tmp->next->prev = baru; // hanya doubly list
    baru->next = tmp->next;
  }

  tmp->next = baru;
  baru->prev = tmp; // hanya doubly list
}
```

5. deleteFirst

konsep: memundurkan data first dan menghapusnya

```c++
void deleteFirst() {
  alamat tmp = first;

  if(first->next == NULL) { // validasi jika hanya memiliki 1 data
    first = NULL;
    last = NULL; // hanya doubly list 
    free(tmp)
    return;
  }

  first->next->prev = NULL; // hanya doubly list
  first = first->next;

  free(tmp);
}
```

6. deleteLast()

konsep: sama seperti deleteFirst namun pada Last, singly list membutuhkan pengulangan

```c++
// doubly list
void deleteLast() {
  alamat tmp = last;

  if(last->prev == NULL) { // validasi jika hanya memiliki 1 data
    first = NULL;
    last = NULL; 
    free(tmp)
    return;
  }

  last->prev->next = NULL;
  last = last->prev;

  free(tmp);
}

// singly list
void deleteLast() {
  alamat tmp = first;

  if(first->next == NULL) { // validasi jika hanya memiliki satu data
    first = NULL;
    free(tmp);
    return;
  }

  while(tmp->next->next != NULL) {
    tmp = tmp->next;
  }

  free(tmp->next);
  tmp->next = NULL;
}
```

7. deleteAfter

konsep: menghapus data yg berada di antara Node setelah data yang dicari dgn pengulangan

```c++
void deleteAfter(int data) { // forward
  alamat tmp = first;
  while(tmp->data != cari && tmp->next != NULL) {
    tmp = tmp->next;
  }

  if(tmp->next->next == NULL) {
   tmp->next = NULL; // validasi jika alamat berikut dari berikutnya kosong
    last = tmp;  // hanya doubly list 
  } else {
    alamat c = tmp->next;
    tmp->next->prev = tmp; // hanya doubly list
    tmp->next = tmp->next->next;
    free(c);
  }
}

void deleteAfter(int data) { // backward - hanya doubly list
  alamat tmp = last;
  while(tmp->data != cari && tmp->prev != NULL) {
    tmp = tmp->prev;
  }

  if(tmp->next->next == NULL) {
   tmp->next = NULL; // validasi jika alamat berikut dari berikutnya kosong
   last = tmp; // hanya doubly list
  } else {
    alamat c = tmp->next;
    tmp->next->prev = tmp; // hanya doubly list
    tmp->next = tmp->next->next;
    free(c);
  }
}
```

8. display / print

konsep: menampilkan semua data linked list dgn pengulangan

```c++
void display() {
  alamat tmp = first;
  while(tmp->next != NULL) {
    cout << tmp->data << endl;
    tmp = tmp->next;
  }
}
```

cmiif

