#include<unistd.h>
#include<stdlib.h>
#include<stdio.h>
#include<stdbool.h>
 

void need(int need[], int p, int Max_need[], int alld[]) {
    for(int i = 0 ;  i < p; i++) {
        need[i] = Max_need[i] - alld[i];
        printf("%d", need[i]);
    }
}
void Safe(int p, int ins, int avail, int Max_Need[], int all[]) 
{
    
    int neeed[p];
    need(neeed, p, Max_Need, all);
    int Sequence[p], seq = 1;
    for(int i = 0 ;  i < p; i++) Sequence[i] = 0;
    bool is_safe = true;
    while(seq <= p) {
        int count = 0;
        for(int i = 0 ; i < p; i++) {
        if(neeed[i] < avail && Sequence[i] == 0) {
            Sequence[i] = seq;
            seq++;
            avail += all[i];
            } else if(Sequence[i] == 0) count++;
        }
        if(count == p) {
            is_safe = false;
            printf("\nnot in Safe State\n\n");
            exit(0);
        }
    }
 
    printf("system in Safe State yes\n");
}
 
int main() {
  int ins, p;
  printf("\nEnter the Number of Intsances of insesource: ");
  scanf("%d", &ins);
  printf("\n");
  printf("Enter total Number of processes : ");
  scanf("%d", &p);
  printf("\n");
  int Max[p];
  for(int i = 0 ;  i < p; i++) {
    printf("Enter Max Number of insesources Need for process p%d : ", i + 1);
    scanf("%d", &Max[i]);
  printf("\n");
 
  int allot[p];
  for(int i = 0 ;  i < p; i++) {
   allot[i] = 0;
  }
  int total = 0;
  for(int i = 0  ; i < p; i++) {
      printf("%d\n", allot[i]);
      total+= allot[i];
  }
 
  printf("%d\n", ins - total);Safe(p, ins, ins - total, Max, allot); 
  return 0;
}
