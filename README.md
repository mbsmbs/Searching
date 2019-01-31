## 검색 (Searching)
```C
//선형 검색
#include <stdio.h>
#include <stdlib.h>

int search(const int a[], int n, int key)
{
    int i = 0; // 반복문에 사용될 변수 선언
    while(1)
    {
        if(i == n) return -1; // 검색 실패
        if(a[i] == key) return i; // 검색 성공
        i++;
    }

    /* for문 사용의 예 (더 짧고 더 간결해집니다.)
    int i;
    for( i = 0; i < n; i++)
    {
        if(a[i] = key)
        {
            return i;
        }
    }
    return -1;
    */
}

int main(int argc, char const *argv[])
{
    int i, nx, ky, idx; 
    int * x;
    
    puts("선형 검색");
    
    printf("요소 개수 : ");
    scanf("%d", &nx); // 요소 갯수 입력 받고 nx로 대입
    
    x = calloc( nx, sizeof(int)); // 요소개수가 nx인 배열 생성
    
    for( i = 0; i < nx; i++)
    {
        printf("x[%d] : ", i);
        scanf("%d", &x[i]); // 생성된 배열에 값을 입력
    }
    
    printf("검색값 : ");
    scanf("%d", &ky); // 검색 값을 입력 받고 ky로 대입
    
    idx = search( x, nx, ky); // 검색한 결과를 받는다. 
    
    if(idx == -1)
    {
        puts("검색에 실패했습니다."); // 검색 실패
    }
    else
    {
        printf("%d는 x[%d]에 있습니다.\n", ky, idx); // 검색 성공
    }

    free(x); // 메모리 해제

    return 0;
}
```

### 보초법
```C
//선형 검색
#include <stdio.h>
#include <stdlib.h>

int search( int a[], int n, int key)
{
    int i = 0; // 반복문에 사용될 변수 선언
    a[n] = key;
    while(1)
    {
        if(a[i] == key) break; // 검색 성공
        i++;
    }
    return i == n ? -1 : i;
}

int main(int argc, char const *argv[])
{
    int i, nx, ky, idx; 
    int * x; // 배열의 첫 번째 요소에 대한 포인터
    
    puts("선형 검색");
    
    printf("요소 개수 : ");
    scanf("%d", &nx); // 요소 갯수 입력 받고 nx로 대입
    
    x = calloc( nx + 1, sizeof(int)); // 요소개수가 nx + 1인 배열 생성
    
    for( i = 0; i < nx; i++)
    {
        printf("x[%d] : ", i);
        scanf("%d", &x[i]); // 생성된 배열에 값을 입력
    }
    
    printf("검색값 : ");
    scanf("%d", &ky); // 검색 값을 입력 받고 ky로 대입
    
    idx = search( x, nx, ky); // 검색한 결과를 받는다. 
    
    if(idx == -1)
    {
        puts("검색에 실패했습니다."); // 검색 실패
    }
    else
    {
        printf("%d는 x[%d]에 있습니다.\n", ky, idx); // 검색 성공
    }

    free(x); // 메모리 해제

    return 0;
}
```
