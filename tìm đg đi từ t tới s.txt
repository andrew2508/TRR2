#include<bits/stdc++.h>
using namespace std;

int a[1001][1001];
vector<int> vt[1001];
int n, s, t;
bool check[1001];
int parent[1001];
bool check2[1001];
int parent2[1001];

void Input(){
    cin>>n>>s>>t;
    for(int i =1;i<=n;i++){
        for(int j =1;j<=n;j++){
            cin>>a[i][j];
            if(a[i][j]){
                vt[i].push_back(j);
            }
        }
    }
    memset(check,false,sizeof(check));
    memset(parent,0,sizeof(parent));
    memset(check2,false,sizeof(check2));
    memset(parent2,0,sizeof(parent2));
}
void DFS(int s){
    check[s] = true;
    for(int x:vt[s]){
        if(!check[x]){
            parent[x] = s;
            DFS(x);
        }
    }
}
void BFS(int s){
    check2[s] = true;
    queue<int> qe;
    qe.push(s);
    while(!qe.empty()){
        int res = qe.front();
        qe.pop();
        for(int x:vt[res]){
            if(!check2[x]){
                parent2[x] = res;
                qe.push(x);
                check2[x] = true;
            }
        }
    }
}
void path(int s, int t){
    int rik = t;
    DFS(s);
    if(check[t]){
        vector<int> pt;
        while(t !=s){
            pt.push_back(t);
            t = parent[t];
        }
        pt.push_back(s);
        cout<<"DFS path: ";
        for(int x:pt) cout<<x<<" ";
        cout<<endl;
    }
    BFS(s);
    if(check2[rik]){
        vector<int> ph;
        while(rik!=s){
            ph.push_back(rik);
            rik = parent2[rik];
        }
        ph.push_back(s);
        cout<<"BFS path: ";
        for(int x:ph) cout<<x<<" ";
        cout<<endl;
    }
    else cout<<"no path"<<endl;
}
int main(){
    Input();
    path(s,t);
    return 0;
}