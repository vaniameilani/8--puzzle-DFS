# 8--puzzle-DFS

Metode DFS adalah salah satu metode algoritma yang melakukan pencarian dari node sebelah kiri hingga bertemu dengan leaf.
Apabila sudah menemukan , maka dapat mencari ke node sebelah kanan atau node tetangga. 
Maka, urutan pencariannya   :
node kiri - root - node kanan. 

Untuk pembahasan kali ini yaitu adalah pada masalah 8-puzzle. 
Berikut adalah penjelasan dari program 8-puzzle dengan pencarian DFS :

1.Bagian dimana untuk memasukkan initial state
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

