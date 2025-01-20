#include<iostream>
#include<windows.h>
#include<conio.h>
#include<fstream>
#include<math.h>
using namespace std;

int  gotoRowCol(int rpos, int cpos)
{
                int xpos=cpos, ypos = rpos;
                COORD scrn;
                HANDLE hOuput = GetStdHandle(STD_OUTPUT_HANDLE);
                scrn.X = cpos;
                scrn.Y = rpos;
                SetConsoleCursorPosition(hOuput, scrn);
}
void sleep(int m)
{
        for(int j=0;j<m*2100000;j++)
        {

        }
}

void programmer(){
gotoRowCol(38, 90);
cout<<"J";sleep(10); cout<<"D";sleep(10); cout<<"_";sleep(10); cout<<"P";sleep(10); cout<<"r";sleep(10); cout<<"o";sleep(10); cout<<"g";sleep(10); cout<<"R";sleep(10); cout<<"@";sleep(10); cout<<"m";sleep(10); cout<<"E";sleep(10); cout<<"R";}
void box(int box_number, int size_box, int & sr,  int & sc, int & er, int & ec)
{
     er = sr + size_box;
     ec = sc + (size_box * 2);
    int k1 = sr, k2 = sc;
    for(sr; sr < er; sr++)
    {
        gotoRowCol(sr, sc);cout<<char(219);
    }
    for(sc; sc <ec; sc++)
    {
        gotoRowCol(er, sc);cout<<char(219);
    }
    for(sc; sc >= k2; sc--)
    {
        gotoRowCol(k1, sc);cout<<char(219);
    }
    for(sr; sr>=k1; sr--)
    {
        gotoRowCol(sr, ec);cout<<char(219);
    }
    gotoRowCol(((sr+er + 1)/2), ((sc + ec + 1)/ 2));
    cout<<box_number;
}
void how_many_box(int & box_number,int & size_box, int  & sr, int & sc, int & er, int & ec)
{
    int k = 1;
    int box_line = sqrt(box_number);
    for (int j = 1; j<= box_line; j++)
    {
        for(int i= 1; i <= box_line; i++)
        {
            sr = k;
            box(box_number,size_box, sr, sc, er, ec);
            sc += (size_box * 2) + 1;
            box_number--;
        }
        k = size_box +k;
        sc = 1;
    }
}
int change_turn(int  turn)
{
    if (turn == 0)
        {
            turn = 1;
        }
        else
        {
            turn = 0;
        }
        return turn;
}
void dice_show(int d)
{
    switch (d)
    {
    case 1:
        gotoRowCol(30, 93);cout<<"       "; gotoRowCol(31, 93);cout<<"   o   "; gotoRowCol(32, 93);cout<<"       ";
        break;
    case 2:
        gotoRowCol(30, 93);cout<<" o   o "; gotoRowCol(31, 93);cout<<"       "; gotoRowCol(32, 93);cout<<"       ";
        break;
    case 3:
        gotoRowCol(30, 93);cout<<"        "; gotoRowCol(31, 93);cout<<"o  o  o "; gotoRowCol(32, 93);cout<<"        ";
        break;
    case 4:
        gotoRowCol(30, 93);cout<<" o   o "; gotoRowCol(31, 93);cout<<"       "; gotoRowCol(32, 93);cout<<" o   o ";
        break;
    case 5:
        gotoRowCol(30, 93);cout<<" o   o "; gotoRowCol(31, 93);cout<<"   o   "; gotoRowCol(32, 93);cout<<" o   o ";
        break;
    case 6:
        gotoRowCol(30, 93);cout<<"o  o  o "; gotoRowCol(31, 93);cout<<"        "; gotoRowCol(32, 93);cout<<"o  o  o ";
        break;
    }
}
int dice_roll_player( int & turn)
{
    int d;
        gotoRowCol(28, 90);
        cout<<"PLAYER TURN : "<<turn + 1;
        while(!kbhit())
            {
            gotoRowCol(26, 90);
            d = rand() % 6 + 1;
            dice_show(d);
            sleep(400000);
            }
        getch();
        gotoRowCol(26, 90);
        d = rand() % 6 + 1;
        dice_show(d);
        return d;
}
int dice_roll_computer(int & turn)
{
    int d, n=0;
        gotoRowCol(28, 90);
        cout<<"COMPUTER TURN : ";
        while(n != 2500)
        {
        gotoRowCol(26, 90);
        d = rand() % 6 + 1;
        dice_show(d);
        sleep(400000);
        n +=1;
        }
        //getch();
        gotoRowCol(26, 90);
        d = rand() % 6 + 1;
        dice_show(d);
        return d;
}
void player_location(int number, int & turn)
{
    int size_box = 4;
    // for finding the row of the number.
    int row = number / 10;
    if (number % 10 == 0)
    {
        row =  (10 - row) * size_box + size_box;
    }
    else
    {
      row = (10 - row) * size_box;
    }
    // For finding the column of the given number.
    int column = number % 10;
    if (number % 10 == 0)
    {
        column = 10;
    }
    column = (11 - column) * (size_box * 2);
    if (turn == 0)
    {
       gotoRowCol(row, column-1);
        cout<<"@";
    }
    else
    {
        gotoRowCol(row, column - 3);
        cout<<"X";
    }
}
// Now we are clearing the last place of pieces.
void Remove_pieces(int number, int & turn)
{
    int size_box = 4;
    // for finding the row of the number.
    int row = number / 10;
    if (number % 10 == 0)
    {
        row =  (10 - row) * size_box + size_box;
    }
    else
    {
      row = (10 - row) * size_box;
    }
    // For finding the column of the given number.
    int column = number % 10;
    if (number % 10 == 0)
    {
        column = 10;
    }
    column = (11 - column) * (size_box * 2);
    if (turn == 0)
    {
       gotoRowCol(row, column-1);
        cout<<" ";
    }
    else
    {
        gotoRowCol(row, column - 3);
        cout<<" ";
    }
}
void snake_ladder(int turn,int & player_score)
{
    // Ladder
    if (player_score == 4)
    {
        player_score = 34; gotoRowCol(20, 90); cout<<"// Player "<<turn + 1<<" : Ladder from 04 to 34";Beep(1000,400);
    }
    if (player_score == 40)
    {
        player_score = 86;gotoRowCol(20, 90); cout<<"// Player "<<turn + 1<<" : Ladder from 40 to 86";Beep(1000,400);
    }
    if (player_score == 75 )
    {
        player_score == 92;gotoRowCol(20, 90); cout<<"// Player "<<turn + 1<<" : Ladder from 75 to 92";Beep(1000,400);
    }
    // SNAKE
    if (player_score == 38)
    {
        player_score = 9;gotoRowCol(20, 90); cout<<"// Player "<<turn + 1<<" : Snake  from 38 to 09";Beep(1000,400);
    }
    if (player_score == 82)
    {
        player_score = 15;gotoRowCol(20, 90); cout<<"// Player "<<turn + 1<<" : Snake  from 82 to 15";Beep(1000,400);
    }
    if (player_score == 97 )
    {
        player_score == 69;gotoRowCol(20, 90); cout<<"// Player "<<turn + 1<<" : Snake  from 97 to 69";Beep(1000,400);
    }
}
void player_pieces_move(int & turn , int & player_score , int & computer)
{
    int n = 0, dice;
    int moves = 0;
    if (computer == 1)
    {
        if(turn == 0)
        {
           dice = dice_roll_player(turn);
        }
        else
        {
            dice = dice_roll_computer(turn);
        }
    }
    else
    {
        dice = dice_roll_player(turn);
    }
    programmer();
    gotoRowCol(25, 90);cout<<"Last Moves: "<<moves<<" ";
    if(player_score < 1)
    {
        if (dice == 6)
        {
            moves = 1;
        }
    }
    if(player_score > 0 || moves == 1)
    {
        while(dice ==6)
        {
            n +=1;
            if (n == 3)
            {
                break;
            }
            moves +=6;
            gotoRowCol(25, 90);cout<<"Last Moves: "<<moves<<" ";
            if (computer == 1)
            {
                if (turn == 0)
                {
                dice = dice_roll_player(turn);
                }
                else {
                dice = dice_roll_computer(turn);
                }
            }else
            {
                dice = dice_roll_player(turn);
            }
            programmer();
        }
        if( n < 3)
        {
            moves += dice;
            gotoRowCol(25, 90);cout<<"Last Moves: "<<moves<<" ";
            if(player_score == 0)
            {
                    Remove_pieces( player_score, turn);
                    player_score = player_score + moves - 6;
                    snake_ladder(turn ,player_score);
            }
            else
            {
                if((player_score + moves) < 101)
                {
                Remove_pieces( player_score,turn);
                  player_score +=moves;
                  snake_ladder(turn, player_score);
                }
            }
            gotoRowCol(25, 90);cout<<"Last Moves: "<<moves<<" ";
        }
    }
}
void game_start(int & turn, int & player_1_score, int & player_2_score, int & computer)
{
    if(turn == 0)
    {
        player_pieces_move(turn , player_1_score, computer);
        gotoRowCol(22,90);
        cout<<"Player 1 score is : "<<player_1_score;
        player_location(player_1_score, turn);
    }
    else
    {
        player_pieces_move(turn , player_2_score, computer);
        gotoRowCol(23,90);
        cout<<"Player 2 score is : "<<player_2_score;
        player_location(player_2_score, turn);
    }
}
void condition_won(int & player_1_score, int & player_2_score,int & computer )
{
    if(player_1_score == 100)
        {
            system("CLS");
            gotoRowCol(25, 70);
            cout<<" Player 1 won the game !!! Well played "; Beep(1200,500);Beep(1200, 500);Beep(1200, 500);Beep(1200, 500);
            gotoRowCol(26, 70);
            cout<<"            C";sleep(70); cout<<"o";sleep(70); cout<<"n";sleep(70); cout<<"g";sleep(70); cout<<"r";sleep(70); cout<<"a";sleep(70); cout<<"t";sleep(70); cout<<"u";sleep(70); cout<<"l";sleep(70); cout<<"a";sleep(70); cout<<"t";sleep(70); cout<<"i";sleep(70); cout<<"o";sleep(70); cout<<"n";sleep(70);
        }
    if(player_2_score == 100)
        {
            system("CLS");
            if(computer == 1)
            {
                gotoRowCol(25, 70); cout<<" Computer won the game !!! weLL played ";Beep(1200,500);Beep(1200, 500);Beep(1200, 500);Beep(1200, 500);
            }else
            {
                gotoRowCol(25, 70); cout<<" Player 2 won the game !!! weLL played ";Beep(1200,500);Beep(1200, 500);Beep(1200, 500);Beep(1200, 500);
            }
            gotoRowCol(26, 70);
            cout<<"            C";sleep(70); cout<<"o";sleep(70); cout<<"n";sleep(70); cout<<"g";sleep(70); cout<<"r";sleep(70); cout<<"a";sleep(70); cout<<"t";sleep(70); cout<<"u";sleep(70); cout<<"l";sleep(70); cout<<"a";sleep(70); cout<<"t";sleep(70); cout<<"i";sleep(70); cout<<"o";sleep(70); cout<<"n";sleep(70);
        }
}
void output(int & player_1_score, int & player_2_score, int & computer)
{
    gotoRowCol(22,90);cout<<"Player 1 score is : "<<player_1_score;
    if (computer == 1)
    {
        gotoRowCol(23,90);cout<<"Computer score is : "<<player_2_score;
    }
    else{
        gotoRowCol(23,90);cout<<"Player 2 score is : "<<player_2_score;
    }
    gotoRowCol(4, 90);cout<<"LADDER : ";
    gotoRowCol(5, 90);cout<<" 04 ----------- 34 ";
    gotoRowCol(6, 90);cout<<" 40 ----------- 86 ";
    gotoRowCol(7, 90);cout<<" 75 ----------- 92 ";
    gotoRowCol(9, 90);cout<<"SNAKE : ";
    gotoRowCol(10, 90);cout<<" 38 ----------- 09 ";
    gotoRowCol(11, 90);cout<<" 82 ----------- 15 ";
    gotoRowCol(12, 90);cout<<" 97 ----------- 69 ";
    gotoRowCol(15, 90);cout<<"SYMBAL : ";
    gotoRowCol(16, 90);cout<<"PLAYER 1 : '@' ";
    gotoRowCol(17, 90);cout<<"PLAYER 2 : 'X' ";
    int n = 81;
    while(n < 127)
    {
        gotoRowCol(1, n);cout<<char(219);gotoRowCol(41, n);cout<<char(219);
        n++;
    } n = 1;
    while(n < 41){
        gotoRowCol(n, 126);cout<<char(219); gotoRowCol(n, 126);cout<<char(219);gotoRowCol(n, 82);cout<<char(219);
        n++;} n = 117;
        int row = 41;
    while(n < 127){
        gotoRowCol(row, n);cout<<char(219);gotoRowCol(row, n-1);cout<<char(219);
        row--; n++;
    }
}
// Now we are working on file handling
void writer(int & player_1_score, int & player_2_score, int & turn)
{
    ofstream writer("file.txt");
    writer<<player_1_score<<" "<<player_2_score<<" " << turn;
}
void reader(int & player_1_score, int & player_2_score, int & turn)
{
    ifstream reader("file.txt");
    reader>>player_1_score>>player_2_score>>turn;
}
int main()
{
    int size_box = 4,box_number = 100, turn = 0;
    int er,ec;
    int player_1_score = 0, player_2_score = 0;
    char  n; int computer;
    gotoRowCol(20, 45);cout<<"Play with computer. Enter '1'  ||  "<<"Two player game. Enter '2'";cin>>computer; system("cls");
    gotoRowCol(25, 70);cout<<"For continue your game.  Enter 'Y' : ";
    cin>>n; system("cls");
    int sr = 1, sc = 1;
    how_many_box(box_number,size_box,sr,sc, er, ec);
    if(n == 'Y' || n == 'y')
    {
        reader(player_1_score, player_2_score, turn);
    }
    while(true)
    {
        output(player_1_score, player_2_score, computer);
        game_start(turn,player_1_score,player_2_score, computer);
        turn = change_turn(turn);
        writer(player_1_score,player_2_score, turn);
        condition_won(player_1_score,player_2_score, computer);
        if(player_1_score == 100 || player_2_score == 100)
        {
            break;
        }
    }
    return 0;
}
