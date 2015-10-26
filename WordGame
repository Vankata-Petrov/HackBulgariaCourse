#include<iostream>
#include<vector>
#include<sstream>
#include<string>
using namespace std;
vector<vector<char> > table;
bool compare(int x,int y,short a,short b,const string &word)
{
    int lenght=1;
    while(lenght!=word.size())
    {
        if(x+a>=0 && x+a<table.size() && y+b>=0 && y+b<=table[x].size())
            {
                if(table[x+a][y+b]==word[lenght]) {lenght++;x+=a;y+=b;}
                else break;
            }
            else break;
    }
    if(lenght==word.size()) return true;
    else return false;
}
int main()
{
    string word;
    int i=0;
    long number=0;
    char letter;
    string row;
    cout<<"Enter the word you're looking for:"<<endl;
    cin>>word;
    cout<<"Now enter the table. Press CTRL+Z on a new line to stop entering!"<<endl;
        while(getline(cin,row))
        {
            vector<char> newVector;
            table.push_back(newVector);
            istringstream rowStream(row);
            while(rowStream>>letter)
            table[i].push_back(letter);
            i++;
        }
    table.erase(table.begin());
    for(int i=0;i<table.size();i++)
    {
        if(table[0].size()!=table[i].size()) {
                cout<<"Wrong input! The table is not rectangular!"<<endl;return 0;}
        for(int j=0;j<table[i].size();j++)
        {
            if(table[i][j]==word[0]) {
                if(compare(i,j,-1,-1,word)) number++;
                if(compare(i,j,-1,0,word)) number++;
                if(compare(i,j,-1,1,word)) number++;
                if(compare(i,j,0,1,word)) number++;
                if(compare(i,j,1,1,word)) number++;
                if(compare(i,j,1,0,word)) number++;
                if(compare(i,j,1,-1,word)) number++;
                if(compare(i,j,0,-1,word)) number++;
            }
        }
    }
    cout<<number<<endl;
    return 0;
}
