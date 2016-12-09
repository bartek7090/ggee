#include <stdio.h>
#include <stdlib.h>
#include "bartek.h"

int ava_waste(int ava, int end_ava);
int ultimate_waste(int ultimates, int end_ultimates);
int bomb_waste(int bomb, int end_bomb);

typedef struct player {
    int ava;
    int ultimates;
    int bomb;
    int end_ava;
    int end_ultimates;
    int end_bomb;
    int player_waste;
    char name[1];

};

int main() {

    player *ptr;
    int num, i, sum = 0;

    printf("Enter group size");
    scanf("%d",&num);
    ptr = (struct player*) malloc(num * sizeof(struct player));

    if(ptr == NULL)
    {
        printf("Error");
        exit(0);
    }

    for(i = 0; i < num; i ++)
    {
        player *p = (ptr + i);
        printf("Enter names of players");
        scanf("%s", &p->name[30]);
        printf("Enter STARTING ultimates, avalanches and energy bombs");
        scanf("%d%d%d", &p->ultimates, &p->ava, &p->bomb);
    }
    for(i = 0; i < num; i ++)
    {
        player *p = (ptr + i);
        printf("Enter ENDING ultimates, avalanches and energy bombs");
        scanf("%d%d%d", &p->end_ultimates, &p->end_ava, &p->end_bomb);
        p->player_waste = (ultimate_waste(p->ultimates, p->end_ultimates))
                          + (ava_waste(p->ava, p->end_ava))
                          + (bomb_waste(p->bomb, p->end_bomb));
    }

    printf("Displaying Infromation:\n");
    for(i = 0; i < num; ++i)
        printf("%s\t%d Gold\t%d\t%d\t%d\n", (ptr+i)->name, (ptr+i)->player_waste ,(ptr+i)->ultimates, (ptr+i)->ava, (ptr+i)->bomb);

    }


int ava_waste(int ava, int end_ava) {
    return ((ava - end_ava) * 45);
}

int ultimate_waste(int ultimates, int end_ultimates){
    return ((ultimates - end_ultimates)* 350);
}

int bomb_waste(int bomb, int end_bomb){
    return ((bomb - end_bomb)* 162);
}


