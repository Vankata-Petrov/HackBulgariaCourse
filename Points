#include<iostream>
using namespace std;
int main()
{
    double x,y;
    short warp=1;
    bool wrong=0;
    cout<<"Please enter 2 numbers only!"<<endl;
    cin>>x>>y;
    string input;
    cout<<"Now enter a string with arrows"<<endl;
    cin>>input;
    for(int i=0;i<input.size();i++)
    {
        if(input[i]=='>') x+=warp;
        else if(input[i]=='<') x-=warp;
        else if(input[i]=='v') y+=warp;
        else if(input[i]=='^') y-=warp;
        else if(input[i]=='~') warp*=-1;
        else {wrong=1;break;}
    }
    if(wrong) cout<<"Wrong input!"<<endl;
    else cout<<"("<<x<<", "<<y<<")"<<endl;
    return 0;
}
