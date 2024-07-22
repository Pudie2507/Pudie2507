#include <bits/stdc++.h>
#define unt unsigned int
#define unll unsigned long long
#define ll long long
#define db double

using namespace std;

vector <int> a[5005];
int qhd[5005][2];
vector <bool> visit(5005,false);

void clearr(int n){
    for (int i=1;i<=n;++i){
        a[i].clear();
        qhd[i][0]=qhd[i][0]=0;
        visit[i]=false;
    }
    for (int i=1;i<n;++i){
        int x,y;cin >> x >> y;
        a[x].push_back(y);
        a[y].push_back(x);
    }
}

//trang la 0, den la 1

void chay(int u){
    visit[u]=true;
    int trtr=0,trd=0,dtr=((a[u].size()*(a[u].size()-1))/2),dd=0;
    for (int i:a[u]){
        if(visit[i]){continue;
        }else{
            chay(i);
            trtr+=qhd[i][0]+1;
            trd+=qhd[i][1];
            dtr+=qhd[i][0];
            dd+=qhd[i][1];
        }
    }
    qhd[u][0]=max(trtr,trd);
    qhd[u][1]=max(dtr,dd);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);



    unt t;cin >> t;
    while (t--){
        unt n;cin >> n;
        clearr(n);
        chay(1);
        cout << max(qhd[1][0],qhd[1][1]) << "\n";
    }

    return 0;
}
