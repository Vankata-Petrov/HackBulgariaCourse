//This code will work only on Windows machines!!!
#include<iostream>
#include<fstream>
#include<unordered_map>
#include<vector>
#include<windows.h>
using namespace std;
bool dirExists(const string& dirName)
{
    DWORD  result = GetFileAttributesA(dirName.c_str());
    if (result == INVALID_FILE_ATTRIBUTES)
        return false;

    if (result & FILE_ATTRIBUTE_DIRECTORY)
        return true;

    return false;
}
void searching(unordered_multimap<string,string> &dataBase,const string &hashWord)
{
    unordered_multimap<string,string>::iterator it;
    vector<string> needToInstall;
    if(!dirExists("./installed_modules")) CreateDirectory("./installed_modules", NULL);
    string dir_path="./installed_modules/"+hashWord;
    if(dirExists(dir_path))
    {
        cout<<hashWord<<" is already installed."<<endl;
        return;
    }
    else
    {
        CreateDirectory(dir_path.c_str(), NULL);
        for(it=dataBase.begin(); it!=dataBase.end(); it++)
        {
            if(it->first==hashWord)
            {
                needToInstall.push_back(it->second);
            }
        }
        cout<<"Installing "<<hashWord<<endl;
        if(needToInstall.size()>1)
        {
            for(int i=0; i<needToInstall.size()-1; i++)
                cout<<"In order to install "<<hashWord<<", we need "<<needToInstall[i]<<", ";
            cout<<" and "<<needToInstall[needToInstall.size()-1]<<"."<<endl;
        }
        else if(needToInstall.size()==1)
        {
            cout<<"In order to install "<<hashWord<<", we need "<<needToInstall[0]<<endl;
            searching(dataBase,needToInstall[0]);
        }
        if(needToInstall.size()>1)
        {
            for(int i=0; i<needToInstall.size(); i++)
            {
                searching(dataBase,needToInstall[i]);
            }
        }
    }
}
int main()
{
    unordered_multimap<string,string> dataBase;
    vector<string> dependencies;
    string str;
    bool quotes=0,square=0;
    string word,hashWord;
    ifstream inputData;
    inputData.open("all_packages.json");
    if(inputData)
    while(1)
    {
        getline(inputData,str);
        for(int j=0; j<str.size(); j++)
        {
            if(str[j]=='"' && square==0)
            {
                quotes=1;
                hashWord="";
                j++;
                while(quotes!=0)
                {
                    if(str[j]=='"' && quotes==1)
                    {
                        quotes=0;
                    }
                    else
                    {
                        hashWord+=str[j];
                        j++;
                    }
                }
            }
            else if(str[j]=='"' && square==1)
            {
                quotes=1;
                j++;
                word="";
                while(quotes!=0)
                    if(str[j]=='"' && quotes==1)
                    {
                        quotes=0;
                        dataBase.insert(make_pair(hashWord,word));
                    }
                    else
                    {
                        word+=str[j];
                        j++;
                    }
            }
            else if(str[j]=='[') square=1;
            else if(str[j]==']') square=0;

        }
        if(str=="}") {inputData.close();break;}
    }
    else {cout<<"Missing all_packages.json!"<<endl;return 0;}
    inputData.open("dependencies.json");
    if(inputData)
        while(1)
        {
        getline(inputData,str);
        for(int j=0; j<str.size(); j++)
        {
            if(str[j]=='"' && square==0)
            {
                quotes=1;
                hashWord="";
                j++;
                while(quotes!=0)
                {
                    if(str[j]=='"' && quotes==1)
                    {
                        quotes=0;
                    }
                    else
                    {
                        hashWord+=str[j];
                        j++;
                    }
                }
            }
            else if(str[j]=='"' && square==1)
            {
                quotes=1;
                j++;
                word="";
                while(quotes!=0)
                    if(str[j]=='"' && quotes==1)
                    {
                        quotes=0;
                        dependencies.push_back(word);
                    }
                    else
                    {
                        word+=str[j];
                        j++;
                    }
            }
            else if(str[j]=='[') square=1;
            else if(str[j]==']') square=0;
            if(hashWord=="dependancies") square=1;
        }
        if(str=="}") {inputData.close();break;}
    }
    else {cout<<"Missing dependencies.json!"<<endl;return 0;}
    for(int i=0; i<dependencies.size(); i++) searching(dataBase,dependencies[i]);
    cout<<"All done."<<endl;
    return 0;
}
