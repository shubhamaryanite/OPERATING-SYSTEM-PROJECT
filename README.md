# OPERATING-SYSTEM-PROJECT
A problem's  solution of the OPERATING SYSTEM questions being given as a project in B-Tech CSE 2nd SEMESTER


/*Design a scheduler that uses a preemptive priority scheduling algorithm based on dynamically changing priority. Larger number for priority indicates higher priority.
Assume that the following processes with arrival time and service time wants to execute (for reference):

ProcessID        	Arrival Time    	Service Time
P1                       	 0                         	 4
P2                       	 1                         	 1
P3                       	 2                         	 2
P4                       	 3                         	 1

When the process starts execution (i.e. CPU assigned), priority for that process changes at the rate of m=1.When the process waits for CPU in the ready queue (but not yet started execution), its priority changes at a rate n=2. All the processes are initially assigned priority value of 0 when they enter ready queue for the first time . The time slice for each process is q = 1. When two processes want to join ready queue simultaneously, the process which has not executed recently is given priority. Calculate the average waiting time for each process. The program must be generic i.e. number of processes, their burst time and arrival time must be entered by user.*/



#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/types.h>
int main() 
{ 

      int i,limit;
	  int total = 0, x, counter = 0;
	  int time_quantum,j; 
      int wait_time = 0, turnaround_time = 0;
	  int pos,z,p[10],prio[10], a_time[10], b_time[10], temp[10],b; 
      float average_wait_time, average_turnaround_time;
      printf("\t\t\t\t\t OPERATING SYSTEM PROJECT \n\n");	
      printf("\t\t\t\t\t QUESTION NUMBER 9\n");
	  printf("\n\t\t\t\t PLEASE PROVIDE FOLLOWING DETAILS FOR SCHEDULING!!\n");
      printf("\nEnter Total Number of Processes for being scheduled :"); 
      scanf("%d", &limit); //limit stores total no of processes enterd by the user for scheduling
      x = limit; 
      
      
      for(i = 0; i < limit; i++) //total details for all processes to be given while calculating
      {
	    p[i]=i+1;
	   
	    prio[i]=0;
	    
            printf("\nEnter total Details of P[%d]\n", i + 1);
            printf("Arrival Time:\t");
            scanf("%d", &a_time[i]);//arrival time
            printf("Burst Time:\t");
            scanf("%d", &b_time[i]); //burst time
            temp[i] = b_time[i];
      }
      
      
      printf("\nEnter the Time Quantum:"); //time quantam
      scanf("%d", &time_quantum); 
      printf("\nProcess ID\t\tBurst Time\t Turnaround Time\t Waiting Time\t Priority\n");
      
      
      for(total = 0, i = 0; x != 0;) 
      { 
		    for(z=0;z<limit;z++)
		    {
			int temp1;
			pos=z;
			for(j=z+1;j<limit;j++)
			{
			    if(prio[j]<prio[pos])
				pos=j;
			}
	temp1=prio[z];
		prio[z]=prio[pos];
		prio[pos]=temp1;
	temp1=b_time[z];
		b_time[z]=b_time[pos];
		b_time[pos]=temp1;
	temp1=a_time[z];
		a_time[z]=a_time[pos];
		a_time[pos]=temp1;
        temp1=p[z];
		p[z]=p[pos];
		p[pos]=temp1;
        temp1=temp[z];
		temp[z]=temp[pos];
		temp[pos]=temp1;
		    }
	if(temp[i] <= time_quantum && temp[i] > 0) 
            { 
                  total = total + temp[i]; 
                  temp[i] = 0; 
                  counter = 1; 
            } 
            else if(temp[i] > 0) 
            { 
                  temp[i] = temp[i] - time_quantum; 
                  total = total + time_quantum; 
            } 
	for(b=0;b<limit;b++)//rate of priorities of processes
            {
			if(b==i)
			prio[b]+=1;//process starts execution
			else
			prio[b]+=2;//process waiting for cpu goes in ready queue
	    }

            if(temp[i] == 0 && counter == 1) 
            { 
                  x--; 
                  printf("\nP[%d]\t\t%d\t\t %d\t\t %d\t\t%d", p[i], b_time[i], total - a_time[i], total - a_time[i] - b_time[i],prio[i]);
                  wait_time = wait_time + total - a_time[i] - b_time[i]; //calculating wait time
                  turnaround_time = turnaround_time + total - a_time[i]; //calculating turnaround time
                  counter = 0; 
            } 
            if(i == limit - 1) 
            {
                  i = 0; 
             }
            else if(a_time[i + 1] <= total) 
            {
                  i++;
	    }
            else 
            {
                  i = 0;
	    }		
      } 
      
      printf("\n\n \t\t Your Program has been terminated \n");
      printf("You have been provided with the solution for your queries regarding scheduling process\n");
      printf("\t\t THANKS FOR GIVING THIS GOLDEN OPPORTUNITY \n");
      printf("\t\t\t\t HAVE A NICE DAY \n");
      return 0; 
}
