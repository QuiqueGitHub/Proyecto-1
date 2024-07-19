# Proyecto-1
#include <iostream>
#include <conio.h>
#include <stdlib.h> //se usa el NEW

using namespace std;

struct nodo{
	int dato;
	nodo *sig;
};

void insertarDatos(nodo *&, int );
void eliminarDatos(nodo *&, int);
void mostrarLista(nodo *);
void listaVacia(nodo *&);
int contarNodos(nodo *&);
int multiNodos(nodo *&, int);
void parImparNodos(nodo *);
void datoEspecifico(nodo *, int);
void cambioNodos(nodo *, int ,int);
//orden ascendente y descendente
void ordenAsce(nodo *&, int);
void ordenDesce(nodo *&, int);
void eliminarPenultimo(nodo *&);
void datosMenores(nodo *&, int, int);



main(){
	nodo *lista = NULL;
	int opc, dato, contaNod, multi, num, c1, c2;//c1 y c2 son cambio 1 y cambio 2
	char orden;
	
	
	do{
		system("cls");
		cout<<"****** MENU LISTA ******"<<endl;
		cout<<"1)Insertar elementos"<<endl;
		cout<<"2)Eliminar datos"<<endl;
		cout<<"3)Mostrar datos"<<endl;
		cout<<"4)Lista vacia? "<<endl;
		cout<<"5)Cantidad de nodos"<<endl;
		cout<<"6)Multiplicacion de los datos"<<endl;
		cout<<"7)Numeros Pares e Impares"<<endl;
		cout<<"8)Nodo especifico"<<endl;
		cout<<"9)Intercambio dos elementos"<<endl;
		cout<<"10)Ordenamiento de nodos"<<endl;
		cout<<"11)Eliminar penultimo nodo"<<endl;
		cout<<"12)Nodos mayores a x"<<endl;
		cout<<"13)SALIR "<< endl;
		cout<<"Seleccionar operacion: \n";
		cin>>opc;
	
	switch(opc){
		case 1:
			cout<<"Ingrese un numero: \n";
			cin>>dato;
			insertarDatos(lista, dato);
			getch();
			break;
		case 2: 
			cout<<"Ingrese dato a eliminar: \n";
			cin>>dato;
			cout<<endl;
			cout<<"Lista ORIGINAL: \n";
			mostrarLista(lista);
			cout<<endl;
			eliminarDatos(lista, dato);
			cout<<"Lista NUEVA: \n";
			mostrarLista(lista);
			cout<<endl;
			getch();
			break;
		case 3:
			cout<<"*****LISTA*****\n";
			mostrarLista(lista);
			getch();
			break;
		case 4:
			cout<<"Estado de la lista: \n";
			listaVacia(lista);
			getch();
			break;
		case 5:
			contaNod = contarNodos(lista);
			cout<<"Cantidad de nodos: "<<contaNod<<endl;
			getch();
			break;
		case 6:
			multi = multiNodos(lista, dato);
			cout<<"Resultado: "<<multi<<endl;
			getch();
			break;
		case 7:
			parImparNodos(lista);
			getch();
			break;
		case 8:
			if(lista == NULL){
				cout<<"La lista esta vacia\n";
			}
			else{
				cout<<"Que dato quiere obtener: \n";
				cin>>dato;
				datoEspecifico(lista, dato);
			}
			getch();
			break;
		case 9:
			cout<<"Lista ORIGINAL: \n";
			mostrarLista(lista);
			cout<<endl;
			cout<<"Seleccione 2 numeros dentro de la lista: \n";
			cout<<"Numero 1:\n";
			cin>>c1;
			cout<<"Numero 2:\n";
			cin>>c2;
			cout<<"Lista CAMBIADA: \n";
			cambioNodos(lista, c1, c2);
			getch();
			break;
		case 10:
			cout<<"Ordenamiento (A)scendente o (D)escendente: \n";
			cin>>orden;
			if(orden == 'a' || orden == 'A'){
				cout<<"Lista ORIGINAL: \n";
				mostrarLista(lista);
				cout<<endl;
				cout<<"Lista ASCENDENTE: \n";
				ordenAsce(lista, dato);
			}
			else if(orden == 'd' || orden == 'D'){
				cout<<"Lista ORIGINAL: \n";
				mostrarLista(lista);
				cout<<endl;
				cout<<"Lista DESCENDENTE: \n";
				ordenDesce(lista, dato);
			}
			else{
				cout<<"Opcion NO valida \n";
			}
			getch();
			break;
		case 11:
			cout<<"Lista ORIGINAL: \n";
			mostrarLista(lista);
			cout<<endl;
			eliminarPenultimo(lista);
			cout<<"Lista sin PENULTIMO: \n";
			mostrarLista(lista);
			getch();
			break;
		case 12:
			cout<<"Ingrese un numero: \n";
			cin>>num;
			cout<<"Nodos que son mayores a "<<num<<endl;
			datosMenores(lista, dato, num);
			getch();
			break;	
	}
		
	}while(opc != 13);
	getch();

	return 0;	
}

void insertarDatos(nodo*&lista, int d){
	nodo *nuevoNodo = new nodo();
	nuevoNodo -> dato = d;
	
	nodo *aux1 = lista;
	nodo *aux2;
	while((aux1 != NULL)){//Si ya hay un dato en la fila y este dato nuevo es menor al anterior
		aux2 = aux1;
		aux1 = aux1 -> sig;
	}
	if(lista == aux1){//Si es el primer dato que se ingresa
		lista = nuevoNodo; //El nodo de lista "absorbe" al dato nuevo
	}
	else{
		aux2 -> sig = nuevoNodo;
	}
	nuevoNodo -> sig = aux1;
	cout<< d << " se inserto correctamente \n";
}

void eliminarDatos(nodo *&lista, int d){
	if(lista != NULL){//Solo si la lista ya tiene al menos un dato
		nodo *auxBorrar;
		nodo *anterior = NULL;
		auxBorrar = lista;
		while((auxBorrar != NULL) && (auxBorrar -> dato != d)){//si  la lista no esta vacia y el dato en el nodo es distinto al buscado
			anterior = auxBorrar; //anterior se vuelve auxBorrar
			auxBorrar = auxBorrar -> sig;//auxBorrar se recorre
		}
		if(auxBorrar == NULL){//Si auxBorrar llega hasta el final
			cout<<"Elemento "<<d<<" no encontrado \n";
		}
		else if(anterior == NULL){
			lista = lista -> sig;
			delete auxBorrar;
		}
		else{
			anterior -> sig = auxBorrar -> sig;
			delete auxBorrar;
		}
	}
}

void mostrarLista(nodo *lista){
	nodo *actual = new nodo();
	actual = lista;
	while(actual != NULL){
		cout<<actual -> dato << " ";
		actual = actual -> sig;//Se recorre el puntero
	}
}

void listaVacia(nodo *&lista){
	if(lista == NULL){
		cout<<"!"<<endl;
	}
	else{
		cout<<"La lista si cuenta con datos \n";
	}
}

int contarNodos(nodo *&lista){
	int contaNod = 0;
	nodo *actual = new nodo();
	actual = lista;
	while(actual != NULL){
		actual = actual -> sig;
		contaNod = contaNod + 1;
	}
	return contaNod;
}

void parImparNodos(nodo *lista){
	nodo *actualPar = new nodo();
	nodo *actualImpar = new nodo();
	actualImpar = lista;
	actualPar = lista;
	int par, impar;
	cout<<"Numeros PARES: \n";
	while(actualPar != NULL){
		par = actualPar -> dato;
		if(par % 2 == 0){
		cout<<actualPar -> dato << " ";
	}
		actualPar = actualPar -> sig;
	}
	cout<<endl;
	cout<<"Numeros IMPARES: \n";
	while(actualImpar != NULL){
		impar = actualImpar -> dato;
		if(impar % 2 != 0){
		cout<<actualImpar -> dato << " ";
	}
		actualImpar = actualImpar -> sig;
	}
		
}

int multiNodos(nodo *&lista, int d){
	int multi = 1;
	nodo *actual = new nodo();
	actual = lista;
	while(actual != NULL){
		multi = multi * actual -> dato;
		actual = actual -> sig;//Recorre
	}
	return multi;
}

void datoEspecifico(nodo *lista, int d){
	bool buscar = false;
	int posi = 0;
	nodo *actual = new nodo();
	actual = lista;

	while((actual != NULL) && (actual -> dato <= d)){
		if(actual -> dato == d){
			buscar = true;
		}
		actual = actual -> sig;
		posi = posi + 1;
	}
	if(buscar == true){
		cout<<"El elemento " << d << " se encuentra en la posicion " << posi<<" dentro de la lista \n";
	}
	else{
		cout<<"El elemento " << d << " NO existe \n";
	}
}

void cambioNodos(nodo *lista, int c1 ,int c2){
	nodo *actual = new nodo();
	actual = lista;
	while(actual != NULL){
		if(actual -> dato == c1){
			actual -> dato = c2;
			cout<<actual -> dato << " ";
		}
		else if(actual -> dato == c2){
			actual -> dato = c1;
			cout<<actual -> dato << " ";
		}
		else{
			cout<<actual -> dato << " ";	
		}
		actual = actual -> sig;
	}
}

void ordenAsce(nodo *&lista, int d){
	nodo *actual = lista;
	nodo *sig = NULL;
	int copia;
	
	if(lista == NULL){//Para comprobar que haya datos en la lista
		listaVacia(lista);
	}
	
	while(actual != NULL){
		sig = actual -> sig;
		while(sig != NULL){
			if(actual -> dato > sig -> dato){ 
				copia = actual -> dato;
				actual -> dato = sig -> dato;
				sig -> dato = copia;	
				/*si el dato es mayor al siguiente, se almacena temporalmente en copia, actual -> dato se recorre y 
				copia se coloca	en sig -> dato que era el nodo enfrente de actual -> dato*/
			}
			sig = sig -> sig;
		}
		actual = actual -> sig;
	}
	mostrarLista(lista);
}

void ordenDesce(nodo *&lista, int d){
	nodo *actual = lista;
	nodo *sig = NULL;
	int copia;
	
	if(lista == NULL){
		listaVacia(lista);
	}
	
	while(actual != NULL){
		sig = actual -> sig;
		while(sig != NULL){
			if(actual -> dato < sig -> dato){
				copia = actual -> dato;
				actual -> dato = sig -> dato;
				sig -> dato = copia;	
				/*si el dato es menor al siguiente, se almacena temporalmente en copia, actual -> dato se recorre y 
				copia se coloca	en sig -> dato que era el nodo enfrente de actual -> dato*/
			}
			sig = sig -> sig;
		}
		actual = actual -> sig;
	}
	mostrarLista(lista);
}



void eliminarPenultimo(nodo *&lista){
	int conta = contarNodos(lista);
	conta = conta - 1;
	if(lista != NULL){//Solo si la lista ya tiene al menos un dato
		nodo *auxBorrar;
		nodo *anterior = NULL;
		auxBorrar = lista;
		while((auxBorrar != NULL) && (auxBorrar -> dato != conta)){//si  la lista no esta vacia y el dato en el nodo es distinto al buscado
			anterior = auxBorrar; //anterior se vuelve auxBorrar
			auxBorrar = auxBorrar -> sig;//auxBorrar se recorre
		}
		if(auxBorrar == NULL){//Si auxBorrar llega hasta el final
			cout<<"La cola esta vacia \n";
		}
		else if(anterior == NULL){
			lista = lista -> sig;
			delete auxBorrar;
		}
		else{
			anterior -> sig = auxBorrar -> sig;
			delete auxBorrar;
		}
	}
}

void datosMenores(nodo *&lista, int d, int n){
	nodo *actual = new nodo();
	actual = lista;
	while(actual != NULL){
			if(actual -> dato > n){
			cout<<actual -> dato << " ";
		}
		actual = actual -> sig;
	}
}
