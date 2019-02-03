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

### 이진검색 (Binary Search)
```C
//이진 검색 ( Binary Search)
#include <stdio.h>
#include <stdlib.h>

int bin_Search(const int a[], int n, int key) // 배열에서 key값과 일치하는 값을 검색하는 이진 검색 함수
{
	int pl = 0;     // 검색한 배열의 맨앞 인덱스
	int pr = n - 1; // 검색한 배열의 맨뒤 인덱스
	int pc;         // 검색한 범위의 중앙 인덱스

	do {
		pc = (pl + pr) / 2; // 중앙 = (맨앞 + 맨뒤) / 2;

		if (a[pc] == key) // 해당 배열의 pc 인덱스 값에 해당하는 값이 key 값과 같은지 확인한다.
		{
			return pc; // 맞으면 pc가 key다
		}
		else if (a[pc] < key) // 해당 배열의 pc 인덱스 값에 해당하는 값이 key 값보다 작으면
		{
			pl = pc + 1; // 맨앞 인덱스 = 중앙 인덱스 + 1
		}
		else
		{
			pr = pc - 1; // 맨앞 인덱스 = 중앙 인덱스 - 1
		}
	} while (pl <= pr); // 맨앞 인덱스가 작거나 같아질때까지 do~while문을 실행한다.

	return -1; // 검색 실패
}

int main()
{
	int i, nx, ky, idx; // 반복문, 요소개수, 키, 인덱스 변수 선언
	int *x; // 메모리 할당을 위한 포인터 선언

	puts("이진 검색");
	printf("요소개수 : ");
	scanf("%d", &nx); // 요소개수를 입력 받아 nx에 대입한다.

	x = calloc(nx, sizeof(int)); // 요소갯수 만큼 메모리 할당
	
	printf("오름차순으로 입력하세요.\n");
	printf("x[0] : ");
	scanf("%d", &x[0]); // 생성된 배열에 첫번째값을 입력한다.

	for (i = 1; i < nx; i++) // 요소갯수만큼 반복
	{
		do {
			printf("x[%d] : ", i);
			scanf("%d", &x[i]); // 첫번째를 제외한 나머지 값을 입력한다. 
		} while (x[i] < x[i - 1]); // 바로 앞 값보다 작으면 다시 입력한다.
	};

	printf("검색값 : ");
	scanf("%d", &ky); // 검색하고자 하는 키값을 입력 받는다.

	idx = bin_search(x, nx, ky); // idx에 배열에 키 값이 있는지 확인 후 값을 대입한다.

	if (idx == -1) // 검색 실패시
	{
		puts("검색에 실패했습니다.");
	}
	else // 검색 성공시
	{
		printf("%d는(은) x[%d]에 있습니다.\n", ky, idx);
	}

	free(x); // 메모리 해제
	
	return 0;
}
```
