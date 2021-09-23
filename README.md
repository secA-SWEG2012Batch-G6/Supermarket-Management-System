void sort() // A function definition containing sort options.

{

	system("cls");

	char *p;

	p = new char;

		cout << "\n\tSORT BY\n\n\t1. Name\n\t2. ID\n \nYour choice: "; // sort options.

		a:

		*p = getch();

	switch(*p)

	{

		case '1':

			sortByname();

			break;

		case '2':

			sortByid();

			break;

		default: cout <<"\a";  goto a;

	}

}

void sortByname()

{

	system("cls");

	char *as;

	as = new char;

	cout << "\n\t1.ASCENDING\n\t2.DESCENDING\n\tYour sort mode: "; // sort mode options.

	aso:

	*as = getch();

	product prod_sort[1000], temp, prod;

	int c=0;

	fstream File;

	File.open("products.dat", ios::binary|ios::in| ios::out);

	if(!File)

	{

		cout << "Error! While opening the file";

		return;

	}

 while(File.read(reinterpret_cast<char *>(&prod_sort[c]), sizeof(product))) // read all available product on an array.

 {

 	c++;

 }

 File.close();

 sortingName(prod_sort, c, *as); // calls a function which sort products by name;

 File.open("products.dat", ios::binary|ios::out);

 if(!File)

 {

 	cerr << "Error!";

 	return;

 }

	for(int f=0; f<c; f++)

	File.write(reinterpret_cast<char *>(&prod_sort[f]), sizeof(product)); // -- writes products sorted by name on the file;

   File.close();

   display();

 delete as;

}



void sortByid()

{

	char *as;

	as = new char;

	cout << "\n\t\t1.ASCENDING\n\t\t2.DESCENDING\n\n\t\tYour sort mode: "; // sort mode.

	aso:

	*as = getch();

	product sort[100], temp, prod;

	int c=0;

	ifstream inFile("products.dat", ios::binary|ios::in);

	if(!inFile)

	{

		cout << "\n\tError!\n";

		return;

	}

  while(inFile.read(reinterpret_cast<char *>(&sort[c]), sizeof(product))) // read product info from file and store it on an array.

  {

  	c++;

  }

  inFile.close();

  sortingId(sort, c, *as);

  ofstream outFile;

  outFile.open("products.dat", ios::binary| ios::out);

  for(int f=0; f<c; f++)

    outFile.write(reinterpret_cast <char *>(&sort[f]), sizeof(product));// writes files sorted by id on the file.

    outFile.close();

    display();

 delete as;

}



void sortingName(product sorting[], int size, char mode)

{

	product temp;

for(int i=0; i<size; ++i)

 {

 	for(int j=i+1; j<size; j++)

 	switch(mode)

 	{

 		case '1':

 		   if(strcmp(sorting[i].retName(), sorting[j].retName()) > 0)

 	     	{

 		     temp = sorting[i];

 		     sorting[i] = sorting[j];

 		     sorting[j] = temp;

 	     	}

 	     	break;

 	    case '2':

 	    	if(strcmp(sorting[i].retName(), sorting[j].retName()) < 0)

 	     	{

 	    	temp = sorting[i];

 		    sorting[i] = sorting[j];

 	    	sorting[j] = temp;

 	     	}

 	    	break;

 	    default: cout << "\a";

 	}

 }



}



void sortingId(product sorting[], int size, char mode) //---- a function definition to sort products by id.

{

	product temp;

 for(int i =0; i<size; i++)

  {

  	for(int j=i+1; j<size; j++)

  	switch(mode)

  	{

  	   case '1':

  	  	 if(strcmp(sorting[i].retId(), sorting[j].retId())>0) // if this condition is fulfilled

  	     	{                                                 // the products are swaped and sorted in ascending order.

  		  	temp = sorting[i];

  		  	sorting[i] = sorting[j];

  		  	sorting[j] = temp;

  	  	   }

         break;

       case '2':

       	if(strcmp(sorting[i].retId(), sorting[j].retId()) <0) // if this condition is fulfilled

       	{                                                     // the products are swaped and sorted in descending order.

       		temp = sorting[i];

       		sorting[i] = sorting[j];

       		sorting[j] = temp;

       	}

       	break;

	  default: cout << "\a wrong mode choice!\n";

     }

  }



}

void viewCategory(char cat[]) // ------ A function  definition to display product with the same category.

{                             //------- It takes Category to be viewed by the user and admin as parameter.

	system("cls");

	product prod;

	bool found = false;

	ifstream inFile;

	inFile.open("products.dat", ios::binary | ios::in);

	if(!inFile)

	{

		cout << "Error! while opening the file\n";

		return;

	}

	cout << "\n\tPRODUCTS WITH THE SAME CATEGORY\n";

	   dispFormat();

	while(inFile.read(reinterpret_cast<char *>(&prod), sizeof(product)))

	{

		if (strcmp(prod.retProd_category(), cat)==0) // if the category of product and category to be viewed ore the same

		{                                            // product information with that category are displayed.

          prod.view();

          found = true;

		}



	}

	inFile.close();

 if(found == false)

 {

 	system("cls");

 	cout << "\n\tNo product found with  " << cat << " category.\n\n";

 }

}



void soldProd(product sold)  //-- A function definition to write sold products on separate binary file.

{

  ofstream outFile;

  outFile.open("sold.dat", ios::binary| ios::app);

  if(!outFile)

  {

  	cout << "\n\tError!\n";

  	return;

  }

  outFile.write(reinterpret_cast<char *>(&sold), sizeof(product));

  outFile.close();

}

void viewSold() //----------- A function definition to read and display sold products for the administrator.

{

	system("cls");

	product sold;

	ifstream inFile;

	inFile.open("sold.dat", ios::binary|ios::in);

	if(!inFile)

	{

		cout << "\n\tError!\n";

		return;

	}

 cout << "\n\n\t\tSold products.\n\n";

    cout <<"\t|"<< setw(12)<<"================================================================================|\n"

      <<"\t|"<< setw(12)<<"Category"<<setw(16)<<"Name"<< setw(16) <<"ID"<< setw(16) <<"Quantity sold"<< setw(16)<<"            Revenue |\n"

      <<"\t|"<<setw(12)<<"================================================================================|\n";



 while(inFile.read(reinterpret_cast<char *>(&sold), sizeof(product)))

 {

 	cout <<"\t|"<< setw(12)<< sold.retProd_category()<<setw(16)<<sold.retName() << setw(16) << sold.retId() << setw(16)<<

   sold.retSold()<< setw(16) <<sold.retRevenue() <<"    |" <<endl;

   cout <<"\t"<<setw(8)<<"|--------------------------------------------------------------------------------|" << endl;



 }

}


