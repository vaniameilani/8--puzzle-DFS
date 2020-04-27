# 8--puzzle-DFS

Metode DFS adalah salah satu metode algoritma yang melakukan pencarian dari node sebelah kiri hingga bertemu dengan leaf.
Apabila sudah menemukan , maka dapat mencari ke node sebelah kanan atau node tetangga. 
Maka, urutan pencariannya   :
node kiri - root - node kanan. 

Untuk pembahasan kali ini yaitu adalah pada masalah 8-puzzle. 
Berikut adalah penjelasan dari program 8-puzzle dengan pencarian DFS :

1.Bagian dimana untuk memasukkan initial state . Inputan ini terdapat pada int main().
```
for(int i = 0; i < 3; i++) {
    for(int j = 0; j < 3; j++) {
      int num; 
	  scanf("%d", &num);
      if(num != 0) in[p++] = num;
      first->state[i][j] = num;
    }
  }
```

2. Bagian dimana untuk memasukkan end state.
```
for(int i = 0; i < 3; i++) {
    for(int j = 0; j < 3; j++) {
      int num; scanf("%d", &num);
      if(num != 0) fin[p++] = num;
      finalState[i][j] = num;
    }
  }
```

3. Setelah itu, program akan memanggil fungsi DFS.
pada int main (), pemanggilannya yang terjadi pada `  dfs();`.
Untuk fungsi DFS nya sendiri yaitu :
```
int ans;
void dfs() {
  int nodes = 0;
  while(!s.empty()) {
    Node* cur = s.top(); s.pop();
    nodes++;
    //printf("%d\n", cur->move);
    if(cmp(cur->state, finalState)) {
      ans = cur->nn;
      getPath(cur);
      return;
    }
    addChilds(cur);
	//print perpindahan blank space '0'
    for(int i = 0; i < 3; i++) {
      for(int j = 0; j < 3; j++) {
		printf("%d ", cur->state[i][j]);
      }
      printf("\n");
    }
    printf("\n");
  }
}
```

4. Pada fungsi diatas terdapat beberapa pemanggilan fungsi-fungsi yang lain 	:
a. fungsi untuk memeriksa apakah initial state sudah mencapat end state yang telah ditentukan sebelumnya. 
```
bool cmp(int a[][3], int b[][3]) {
  for(int i = 0; i < 3; i++) {
    for(int j = 0; j < 3; j++) {
      if(a[i][j] != b[i][j])
	return false;
    }
  }
  return true;
}
```
b. Apabila belum mencapai end state , maka program akan memanggil fungsi `getPath` untuk berpindah ke node selanjutnya.
```
void getPath(Node* cur) {
  Node* par = cur;
  while(par != NULL) {
    path.push_front(par->move);
    par = par->par;
  }
}
```
c. jalur/path yang telah diperiksa tersebut atau dilewati ditambahkan sebagai child dengan memanggil fungsi pada `addChild`.
```
void addChilds(Node* cur) {
  pii pos0 = find0(cur->state);
  int i = pos0.F, j = pos0.S;
  
  Node* node2 = new Node();
  Node* node4 = new Node();
  Node* node6 = new Node();
  Node* node8 = new Node();
  fill(node2, cur); fill(node4, cur); fill(node6, cur); fill(node8, cur);
  node2->par = cur; node4->par = cur; node6->par = cur; node8->par = cur;
  node2->nn = cur->nn + 1; node4->nn = cur->nn + 1; node6->nn = cur->nn + 1; node8->nn = cur->nn + 1;
  
  if(i != 0) {
    move2(node2, i, j);
    node2->move = Up;
    if(!visited(node2))
      s.push(node2);
  }
  if(j != 0) {
    move4(node4, i, j);
    node4->move = Left;
    if(!visited(node4))
      s.push(node4);
  }
  if(i != 2) {
    move8(node8, i, j);
    node8->move = Down;
    if(!visited(node8))
      s.push(node8);
  }
  if(j != 2) {
    move6(node6, i, j);
    node6->move = Right;
    if(!visited(node6))
      s.push(node6);
  }
}
```
5. Kemudian, ada beberapa fungsi lainnya	:
a. Fungsi untuk memeriksa apakah  path tersebut telah dilewati atau belum
```
bool visited(Node* a) {
  Node* par = a->par;
  while(par != NULL) {
    if(cmp(a->state, par->state)) return true;
    par = par->par;
  }
  
  return false;
}
```
b. Fungsi untuk mengisi node yang akan menjadi child(new node) dengan node saat ini.
```
void fill(Node* a, Node* b) {
  for(int i = 0; i < 3; i++) {
    for(int j = 0; j < 3; j++) {
      a->state[i][j] = b->state[i][j];;
    }
  }
}
```

c. Untuk pergerakan blank space ke atas
```
void move2(Node* a, int i, int j) {
  //i - 1
  a->state[i][j] = a->state[i - 1][j];
  a->state[i - 1][j] = 0;
}
```
d. Untuk pergerakan blank space ke kiri
```
void move4(Node* a, int i, int j) {
  //j - 1
  a->state[i][j] = a->state[i][j - 1];
  a->state[i][j - 1] = 0;
}
```
e. Untuk pergerakan blank space ke kanan
```
void move6(Node* a, int i, int j) {
  //j + 1
  a->state[i][j] = a->state[i][j + 1];
  a->state[i][j + 1] = 0;
}
```
f. Untuk pergerakan blank space ke bawah
```
void move8(Node* a, int i, int j) {
  //i + 1
  a->state[i][j] = a->state[i + 1][j];
  a->state[i + 1][j] = 0;
}
```
