<pre>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct node
{
    char name[4];
    int x;
    int y;
    int c_time;
    int ta;
    int w_t;
};
void take_input_aditya(struct node *temp, int n)
{
    for (int i = 0; i < n; i++)
    {
        printf("enter the name ,arrival time and burst time\n");
        scanf("%s %d %d", ((temp + i)->name), &((temp + i))->x, &(temp + i)->y);
        // printf("%s,%d,%d\n",((temp+i)->name),((temp+i))->x,(temp+i)->y);
    }
}
void sorting(struct node *temp, int n)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = i + i; j < n; j++)
        {
            if (temp[i].x > temp[j].x || (temp[i].x == temp[j].x && temp[i].y > temp[j].y))
            {
                int help1 = temp[i].x;
                temp[i].x = temp[j].x;
                temp[j].x = help1;
                help1 = temp[i].y;
                temp[i].y = temp[j].y;
                temp[j].y = help1;
                char *help = (char *)malloc(4 * sizeof(char));
                strcpy(help, temp[i].name);
                strcpy(temp[i].name, temp[j].name);
                strcpy(temp[j].name, help);
                free(help);
            }
        }
    }
    return;
}
void sjf_preemtive(struct node *temp, int n)
{
    sorting(temp, n);
    int help = 0;
    float wt = 0, t_around = 0;
    temp[0].c_time = temp[0].x + temp[0].y + help;
    temp[0].ta = temp[0].c_time - temp[0].x;
    t_around += (float)(temp[0].ta);
    temp[0].w_t = temp[0].ta - temp[0].y;
    wt += (float)(temp[0].w_t);
    help = temp[0].x + temp[0].y;
    printf("%s %d %d %d %d %d\n", temp[0].name, temp[0].x, temp[0].y, temp[0].c_time, temp[0].ta, temp[0].w_t);
    for (int i = 1; i < n; i++)
    {
        temp[i].c_time = temp[i].y + help;
        help = temp[i].c_time;
        temp[i].ta = temp[i].c_time - temp[i].x;
        t_around += (float)(temp[i].ta);
        temp[i].w_t = temp[i].ta - temp[i].y;
        wt += (float)(temp[i].w_t);
        printf("process no ,arrival time,burst time ,completion time , TAT, WT, RT\n");
        printf("%s %d %d %d %d %d\n", temp[i].name, temp[i].x, temp[i].y, temp[i].c_time, temp[i].ta, temp[i].w_t);
    }
    printf("average turnaround time is %f: \n", t_around / n);
    printf("average waiting time is %f : \n", wt / n);
    printf("average throughput time is %f:\n", (float)(temp[n - 1].c_time) / n);
}
int main()
{
    int n;
    printf("enter the number process: \n");
    scanf("%d", &n);
    struct node sjf[n];
    take_input_aditya(sjf, n);
    sjf_preemtive(sjf, n);
}
</pre>

<pre>
#include <stdio.h>
#define MAX_FRAMES 10

int main()
{
    int frames[MAX_FRAMES], pages[MAX_FRAMES];
    int num_frames, num_pages, page_faults = 0, hit = 0, i, j, k, min;
    printf("Enter number of frames: ");
    scanf("%d", &num_frames);
    printf("Enter number of pages: ");
    scanf("%d", &num_pages);
    printf("Enter the reference string: ");
    for(i = 0; i < num_pages; ++i)
        scanf("%d", &pages[i]);
    for(i = 0; i < num_frames; ++i)
        frames[i] = -1; // initialize all frames to -1 (empty)
    for(i = 0; i < num_pages; ++i)
    {
        for(j = 0; j < num_frames; ++j)
        {
            if(frames[j] == pages[i]) // check if page is already in frame
            {
                hit = 1; // page hit
                break;
            }
        }
        if(hit == 0) // page fault
        {
            min = 9999;
            for(j = 0; j < num_frames; ++j) // find the least recently used page
            {
                for(k = i - 1; k >= 0; --k)
                {
                    if(frames[j] == pages[k])
                    {
                        if(k < min)
                        {
                            min = k;
                            break;
                        }
                    }
                }
                if(k < 0)
                {
                    min = j;
                    break;
                }
            }
            frames[min] = pages[i]; // replace the least recently used page
            ++page_faults;
        }
        hit = 0;
        printf("\n");
        for(j = 0; j < num_frames; ++j) // print the current state of frames
        {
            printf("%d\t", frames[j]);
        }
    }
    printf("\nTotal Page Faults = %d", page_faults);
    return 0;
}

</pre>
