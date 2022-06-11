# CLAP3
## Counting Sundays
```
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

const unsigned int Sunday = 1;
unsigned int getWeekday(unsigned long long year, unsigned int month, unsigned int day){
    if (month <= 2){
    month += 12;
    year--;
  }
  return (day +
          13 * (month + 1) / 5 +
          year + year / 4 - year / 100 + year / 400)
         % 7;
}
void swapy(unsigned long long* x,unsigned long long* y){
    int newvar=*x;
    *x=*y;
    *y=newvar;
}
void swapm(unsigned int* x,unsigned int* y){
    int newvar=*x;
    *x=*y;
    *y=newvar;
}

int main()
{
  unsigned int tests;
  scanf("%u",&tests);
  while (tests--)
  {
    unsigned long long year1, year2;
    unsigned int month1, month2, day1, day2;
    scanf("%llu %u %u",&year1,&month1,&day1);
    scanf("%llu %u %u",&year2,&month2,&day2);
    if (year2 < year1 || (year2 == year1 && month2 < month1))
    {
      swapy(&year1,&year2);
      swapm(&month1,&month2);
    }
    unsigned long long currentYear  = year1;
    unsigned int currentMonth = month1;
    if (day1 > 1)
    {
      currentMonth++;
      if (currentMonth > 12)
      {
        currentMonth -= 12;
        currentYear++;
      }
    }
    unsigned int sum = 0;
    while (currentYear + 2800 < year2)
    {
      currentYear += 2800;
      sum += 4816;        
    }
    while (currentMonth < month2 || currentYear < year2) 
    {
      if (getWeekday(currentYear, currentMonth, 1) == Sunday)
        sum++;
      currentMonth++;
      if (currentMonth > 12)
      {
        currentMonth -= 12;
        currentYear++;
      }
    }
    if (getWeekday(currentYear, currentMonth, 1) == Sunday)
      sum++;
    printf("%u\n",sum);
  }
  return 0;
}

```

## Calculate the Nth term
```
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>
int find_nth_term(int n, int a, int b, int c) {
    if(n==1){
        return a;
    }else if(n==2){
        return b;
    }else if(n==3){
        return c;
    }else{
        return find_nth_term(n-1,a,b,c)+find_nth_term(n-2,a,b,c)+find_nth_term(n-3,a,b,c);
    }
}
int main() {
    int n, a, b, c;
    scanf("%d %d %d %d", &n, &a, &b, &c);
    int ans = find_nth_term(n, a, b, c);
    printf("%d", ans); 
    return 0;
}
```

## Amicable Numbers
```
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>
#include <stdbool.h>
#define N 100001
int main(void){
    bool *sieve=(bool *)malloc(N*sizeof(bool));
    sieve[0]=false;
    sieve[1]=false;
    for(int i=2;i<N;i++){
        sieve[i]=true;
    }
    int rcn=sqrt(N);
    for(int i=2;i<=rcn;i++){
        for(int j=2*i;j<N;j+=i){
            sieve[j]=false;
        }
    }
    int *primeFactors=(int *)malloc((N/2)*sizeof(int));
    int count=0;
    for( int i=0;i<N;i++){
        if(sieve[i]){
            primeFactors[count++]=i;
        }
    }
    primeFactors=realloc(primeFactors,count*sizeof(int));
    int *amicable=(int *)malloc(N*sizeof(int));
    amicable[0]=0;
    for(int i=1;i<N;i++){
        int number=i;
        int sum=1;
        int index=0;
        while(number>1){
            int power=0;
            while(number%primeFactors[index]==0){
                number/=primeFactors[index];
                power++;
            }
            sum*=(pow(primeFactors[index],power+1)-1)/(primeFactors[index]-1);
            index++;
        }
        amicable[i]=sum-i;
    }
    int repetition,n,amicaTest,k=0;
    scanf("%d",&repetition);
    while(k<repetition){
        int amicaSum=0;
        scanf("%d",&n);
        int i=1;
        while(i<n){
            amicaTest=amicable[i];
            if(amicaTest <N){
            if(i==amicable[amicaTest] && i!=amicaTest ){  
                amicaSum+=i;
            }
            }
            i++;       
        }
    printf("%d\n",amicaSum);
    k++;
    }
return 0;
}
```

## Alternating Characters
```
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>
int main(){
    int t;
    long i=0;
    unsigned int count=0;
    char * c;
    scanf("%d",&t);
    c=(char *)malloc(sizeof(char)*(100002));
    while(t--){
        scanf("%s",c);
        for(i=0; *(c+i); i++){
            if(c[i]==c[i+1]){
                count++;
            }
        }
        printf("%u\n",count);
        count=0;
    }
    return 0;
}
```

## Number Spiral Diagonals
```
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

unsigned int powmod(unsigned long long base, unsigned int exponent, unsigned int modulo)
{
  unsigned long long result = 1;
  while (exponent > 0)
  {
    if (exponent % 2 == 1)
    {
      result = (result * base) % modulo;
      exponent--;
    }
    else
    {
      base = (base * base) % modulo;
      exponent /= 2;
    }
  }
  return result;
}

unsigned int inverseModulo(unsigned int a, unsigned int modulo)
{
  return powmod(a, modulo - 2, modulo);
}

int main()
{
  unsigned int tests;
  scanf("%i", &tests);
  while (tests--)
  {
    unsigned long long n;
    scanf("%llu", &n);

  
    unsigned long long sum = 1;
      
    unsigned long long x = n / 2;
    const unsigned int Modulo = 1000000007;

    x %= Modulo;

  
    unsigned long long sharedTerm = (2*x * (x + 1)) % Modulo;

    
    unsigned long long sum1 = ((4 * sharedTerm * (2*x + 1)) % Modulo) * inverseModulo(3, Modulo);

   
    unsigned long long sum2 = sharedTerm + 4*x + 1;

    
    sum = (sum1 % Modulo + sum2 % Modulo) % Modulo;

    printf("%lld", sum);
    printf("\n");
  }
  return 0;
}
```
