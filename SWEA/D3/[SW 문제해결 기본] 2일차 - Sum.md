## [문제]
다음 100X100의 2차원 배열이 주어질 때, 각 행의 합, 각 열의 합, 각 대각선의 합 중 최댓값을 구하는 프로그램을 작성하여라.
다음과 같은 5X5 배열에서 최댓값은 29이다.

<img width="361" height="295" alt="image" src="https://github.com/user-attachments/assets/6710f53d-43ba-432c-97db-128ffd0cf5ac" />


## [제약 사항]
총 10개의 테스트 케이스가 주어진다.
배열의 크기는 100X100으로 동일하다.
각 행의 합은 integer 범위를 넘어가지 않는다.
동일한 최댓값이 있을 경우, 하나의 값만 출력한다.
 
## [입력]
#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스의 답을 출력한다.

입력
1
13 24 13 24 1 7 24 11 22 18 22 16 24 8 15 28 9 24 14 14 28 18 17 9 3 29 22 12 28 2 25 6 11 26 14 19 3 26 13 6 23 3 3 29 13 25 4 27 8 25 28 8 9 17 28 13 24 27 9 25 21 20 6 16 28 5 22 11 9 29 13 26 28 2 11 10 14 14 5 11 26 9 15 3 23 9 8 11 12 6 9 18 6 14 28 21 24 24 20 12
20 28 29 21 27 13 29 16 6 28 5 7 13 20 7 1 11 1 23 12 4 9 27 19 26 2 21 2 1 18 4 20 6 4 18 9 20 3 28 28 1 21 1 2 11 7 20 15 7 29 14 7 15 10 29 24 2 25 29 3 11 9 17 6 2 17 17 11 7 20 26 10 8 1 15 10 2 29 7 9 17 8 25 28 29 12 28 19 3 4 17 17 28 9 2 15 14 6 20 3
13 19 28 23 11 1 19 5 5 28 19 18 16 14 26 20 6 12 20 18 16 22 25 21 25 29 3 ............
........
........
 
## [출력]
#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스의 최고점과 최저점의 높이 차를 출력한다.

출력
#1 1712
#2 1743
.......
.......

## [풀이]

```java

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

class Solution {
    public static void main(String args[]) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        
        // SWEA Sum 문제는 테스트 케이스가 10개로 고정되어 있습니다.
        for(int test_case = 1; test_case <= 10; test_case++){
            String line = br.readLine();
            if (line == null) break;
            int Num = Integer.parseInt(line.trim());
            
            int[][] arr = new int[100][100];
            
            // 100x100 배열 입력 받기 (공백 단위로 안전하게 토큰 분리)
            for(int i = 0; i < 100; i++){
                for(int j = 0; j < 100; j++){
                    while (st == null || !st.hasMoreTokens()) {
                        String l = br.readLine();
                        if (l == null) break;
                        st = new StringTokenizer(l);
                    }
                    arr[i][j] = Integer.parseInt(st.nextToken());
                }
            }
            
            int max = 0;
            
            // 1. 행 합
            for(int i = 0; i < 100; i++){
                int rowSum = 0;
                for(int j = 0; j < 100; j++){
                    rowSum += arr[i][j];                    
                }
                if(rowSum > max){
                    max = rowSum;
                }
            }
            
            // 2. 열 합
            for(int j = 0; j < 100; j++){
                int colSum = 0;
                for(int i = 0; i < 100; i++){
                    colSum += arr[i][j];
                }
                if(colSum > max){
                    max = colSum;
                }
            }
            
            // 3. 대각선 합
            int diag1Sum = 0;
            int diag2Sum = 0;
            for(int i = 0; i < 100; i++){
                diag1Sum += arr[i][i];
                diag2Sum += arr[i][99 - i];
            }
            if(diag1Sum > max){
                max = diag1Sum; 
            }
            if(diag2Sum > max){
                max = diag2Sum; 
            }
            
            System.out.println("#" + test_case + " " + max);
        }
    }
}
```

## [다른 풀이]
Scanner로 원래 안 풀리는 문제인지 모르겠다만 Scanner만 사용했을 때 코드

```java
import java.util.*;
import java.io.FileInputStream;

class Solution{
    public static void main(String args[]) throws Exception{

        Scanner sc = new Scanner(System.in);
        int T;
        T = sc.nextInt();
        for(int test_case = 1; test_case <= T; test_case++){
            int Num = sc.nextInt();
            int[][] arr = new int[100][100];
            for(int i = 0; i < 100; i++){
                for(int j = 0; j < 100; j++){
                    arr[i][j] = sc.nextInt();
                }
            }
            int max = 0;
            for(int i = 0; i < 100; i++){
                int rowSum = 0;
                for(int j = 0; j < 100; j++){
                    rowSum += arr[i][j];                    
                }
                if(rowSum > max){
                    max = rowSum;
                }
            }
            for(int j = 0; j < 100; j++){
                int colSum = 0;
                for(int i = 0; i < 100; i++){
                    colSum += arr[i][j];
                }
                if(colSum > max){
                    max = colSum;
                }
            }
            int diag1Sum = 0;
            int diag2Sum = 0;
            for(int i = 0; i < 100; i++){
                diag1Sum += arr[i][i];
                diag2Sum += arr[i][99 - i];
            }
            if(diag1Sum > max){
                max = diag1Sum; 
            }
            if(diag2Sum > max){
                max = diag2Sum; 
            }
            
            System.out.println("#" + test_case + " " + max);
        }
    }
}
```
