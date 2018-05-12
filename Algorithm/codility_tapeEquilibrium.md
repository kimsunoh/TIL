# Problem Link
- [link](https://app.codility.com/programmers/lessons/3-time_complexity/tape_equilibrium/)

## 풀이
```java
public static int tapeEquilibrium_solution(int[] A) {
    int gap = 0;

    /**
    * firstIdx와 maxIdx를 비교하며 gap을 구하며 중간으로 수렴
    * 중간치의 gap을 반환
    */
    int firstIdx = 0;
    int lastIdx = A.length-1;

    while( firstIdx < lastIdx ) {
        if( gap == 0 ) {
            gap += A[firstIdx++] - A[lastIdx--];
        } else if( Math.abs(gap - A[lastIdx]) < Math.abs(gap + A[firstIdx]) ) {
            gap -= A[lastIdx];
            lastIdx--;
        } else {
            gap += A[firstIdx];
            firstIdx++;
        }
    }

    if( lastIdx == firstIdx )
        if( Math.abs(gap - A[lastIdx]) < Math.abs(gap + A[firstIdx]) ) {
            gap -= A[lastIdx];
        } else {
            gap += A[firstIdx];
        }

    return Math.abs(gap);
}
```