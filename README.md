//# Supermarket-Management-System
#include<iostream>
#include<cstring>

using namespace std;
void create_product(string& a, double& n, double& x);
void show_all_product(string& a, double& n, double& x);
void menu();
void admin_menu();
void cusomer_menu();
int main()
{
    string name;
    double age;
    double price;
    menu();
    admin_menu();
    create_product(name,age);
    cout<<"showing lists\n";
    show_all_product(name,age);

    return 0;
}
void create_product(string& a, double& n, double& x ) {

    cout << "input your product name\n";
    cin>>a;
    cout<<"input product id\n";
    cin>>n;
    cout<<"input product price\n";
    cin>>x

}
void show_all_product(string& a, double& n) {


    cout<<"your name is "<<a<<endl;
    cout<<"your age is "<<n;
}

void menu() {
    int y;
    cout<< "MAIN MENU\n";
    cout<<"admin_menu\n";
    cout<<"Customer menu\n";
    cin>>y;
    switch(y) {

    case 1 :
        void admin_menu();
        break;
    case 2 :
        void customer_menu();
        break;
    default:
        cout<<"INCORRECT INPUT", return 0;
    }
}
void admin_menu() {
    int option;
    cout<<"admin menu\n";
    cout<<"enter 1 to create product\n";
    cout<<"enter 2 to list all products\n";
    cin>>option;
    switch(option) {
    case 1:
        create_product();
        break;
    case 2:
        show_all_product();
        break;
    }
}
void customer_menu() {
    int k;
    cout<<"WELCOME TO OUR SUPERMARKET\n";
    cout<<"1.to see all products in our store\n";
    cout<<"2.to see the most expensive items in our store\n";
    cout<<"3.exit\n";
    cin>>k;
    switch(k) {
    case 1 :
        void show_all_product();
        break;
    case 2 :if(price>500){
    cout<<products
    }
        break;
    default:
        cout<<endl;
        return 0;
    }



}
