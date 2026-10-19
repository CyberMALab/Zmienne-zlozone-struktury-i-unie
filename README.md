# Zmienne złożone – struktury i unie
## **Struktury**
Zmienną złożoną, którą zdecydowanie warto znać jest struktura. Budowanie struktur pozwala nam łączyć ze sobą różne zmienne w spójny obiekt. Daje nam to możliwość logicznego powiązania wielu zmiennych. Ułatwia to tworzenie programów, wewnątrz których wykorzystujemy wiele zmiennych definiujących ten sam obiekt. Przykładem takiego obiektu może być punkt. Aby zdefiniować punkt w dwuwymiarowym układzie współrzędnych, potrzebujemy znać poszczególne współrzędne punktu. Struktura pozwoli nam je połączyć logicznie w jedną strukturę. Aby zadeklarować taką strukturę, należy zacząć od podania słowa kluczowego *struct* oraz nadania identyfikatora (nazwy). W naszym przypadku za identyfikator przyjmiemy słowo „punkt”. Następnie otwieramy nawias klamrowy, deklarujemy zmienne składowe, a całość zamykamy średnikiem.  

*Przykład (11.0) struktura punkt*

```
struct punkt
{
	float x;
	float y;	
};
```

Taką strukturę należy deklarować przed pierwszym miejscem, w którym tworzona jest zmienna typu struktury (zaleca się nad main).

Kiedy struktura jest już zdefiniowana, należy zadeklarować zmienną typu *struct*. Robi się to analogicznie jak deklaracja zmiennej prostej, tyle że naszym typem jest struktura. W praktyce więc podajemy słowo kluczowe *struct* , identyfikator struktury oraz nadajemy identyfikator zmiennej. Po takiej deklaracji mamy zadeklarowaną zmienną złożoną, więc utworzone są również jej zmienne składowe. Aby uzyskać dostęp do składowych zmiennej złożonej typu *struct* należy użyć operatora `.`. Operatora tego używa się w połączeniu dwóch identyfikatorów – identyfikatora zmiennej złożonej oraz identyfikatora zmiennej składowej struktury. Zmienne złożone *struct*, można podawać jako parametr funkcji oraz jako tym samej funkcji. W języku C jest również zdefiniowane wykonanie operacji przypisania dwóch zmiennych *struct* tego samego typu. Przypisanie powoduje skopiowanie wszystkich wartości odpowiednich zmiennych składowych. 

*Przykład (11.1) program obsługujący strukturę punkt*

```
#include <stdio.h>
#include <stdlib.h>

struct punkt
{
	float x;
	float y;	
};
struct punkt wczytaj_punkt();
void wyswietl_punkt(struct punkt point);

int main() {
	struct punkt point; /* Deklaracja zmiennej złożonej point */
/* Przypisanie struktury tego samego typu do innej struktrury spowoduje skopiowanie wszystkich jej zmiennych składowych */
	point = wczytaj_punkt();
	wyswietl_punkt(point);	
	return 0;
}
struct punkt wczytaj_punkt()
{
	struct punkt tmp;
/* odwołanie się do poszczególnych zmiennych składowych przy użyciu '.' */
	printf("Podaj wspolrzedna x: ");
	scanf(" %f", &tmp.x);
	printf("Podaj wspolrzedna y: ");
	scanf(" %f", &tmp.y);
	return tmp;
	
}
void wyswietl_punkt(struct punkt pkt)
{
/* odwołanie się do poszczególnych zmiennych składowych przy użyciu '.' */
	printf("(%5.2f,%5.2f)",pkt.x,pkt.y); /* identyfikator.identyfikator*/

}
```

Zmiennej złożonej *struct*, można nadać wartości początkowe. Jest to bardzo podobne do nadawania wartości początkowych tablicy, bowiem wykonuje się to analogicznie.

*Przykład (11.2) przypisanie wartości początkowych zmiennej złożonej.*

```
/* point.x=3.23 point.y=5.33 */
struct punkt point = {3.23f,5.33f};
```

## **Unie**
Unia, to zmienna przechowujące pojedynczy obiekt pamięci, którego typ może ulec zmianie w trakcie działania programu. Aby zadeklarować unię, należy wykonać analogiczne kroki co w przy tworzeniu struktury. To samo jeśli chodzi o deklaracje zmiennej złożonej *union*. Jedyną różnicą i to znaczną, jest użycie zmiennej *union*.  Zmienna taka może przechowywać jednocześnie dane o tylko jednej z zadeklarowanych wartości. Bardzo dobrze prezentuje to przykład (11.2), w którym można zauważyć, że po zmianie parametru zmiennoprzecinkowego *f\_val* wartość *i\_val* uległa zmianie. Dzieje się tak, ponieważ zmienna *f\_val* i *i\_val* korzysta z tej samej przestrzeni pamięci.

*Przykład (11.3) zmiana parametrów składowych unii*

```
#include <stdio.h>
#include <stdlib.h>


union u_tag
{
	int i_val;
	float f_val;
};

int main() 
{
	union u_tag u;
	u.i_val = 3;
	printf("int=%12d ; float=%12.1lf \n", u.i_val,u.f_val);
	u.f_val = 3.33;
	printf("int=%12d ; float=%12.1lf \n", u.i_val,u.f_val);
	return 0;
}
```

*Wynik działania programu*

>int=           3 ; float=         0.0
>
>int=  1079320248 ; float=         3.3


*Schemat (11.0) różnica w wykorzystaniu pamięci struktura i unia* 

![union vs struct](https://user-images.githubusercontent.com/71324202/145053551-3409927d-b3ea-48d6-8342-8a77a40fdf56.png)


## **Własne typy wyliczeniowe *enum***
Typ wyliczeniowy, wykorzystywany jest do ułatwienia czytania  kodu. W praktyce zmienne typu *enum* są zmiennymi całkowitoliczbowymi (*int*). Jedyną różnicą jest to, że przypisujemy odpowiedni identyfikator do liczby (coś podobnego jak zbudowane są znaki char w ASCII). Pozwala nam to łatwiej poruszać się po własnym kodzie, w przypadku tworzenia dużych programów. Aby zadeklarować własny typ wyliczeniowy zaczynamy od słowa kluczowego *enum.* Następnie nadajemy identyfikator typu oraz jego argumenty w nawiasie klamrowym. Wszystko zamykamy średnikiem.

*Przykład (11.4) własny typ wyliczeniowy – kolory*

```
#include <stdio.h>
#include <stdlib.h>

enum COLORS{COL_WHITE,COL_RED,COL_BLUE,COL_YELLOW,COL_BLACK };

int main() 
{
	enum COLORS shape_color;
	return 0;
}
```

Przykład (11.3) pokazuje w jaki sposób stworzyć własny typ wyliczeniowy oraz utworzyć zmienną korzystającą z tego typu. W praktyce zmienna *shape\_color* jest zmienną całkowitoliczbową, jedna można do niej przypisywać argumenty korzystając z identyfikatorów wyliczeniowych. Każdy identyfikator ma również przypisaną swoją liczbę. W przykładzie *COL\_WHITE* jest tak naprawdę wartością 0, *COL\_RED* wartością 1, a *COL\_BLACK* wartością 4. W momencie tworzenia typu wyliczeniowego możemy przypisać wartości jakie będą przypisane do naszych identyfikatorów poprzez dodanie znaku równości i liczby, z którą będzie powiązana.

*Przykłady – różna deklaracja typów wyliczeniowych*

*(11.5)*  

```
/* ten sam efekt co w przykładzie 11.3 */
enum COLORS{
	COL_WHITE=0,		/* COL_WHITE = 0*/
	COL_RED=1,		/* COL_RED = 1*/
	COL_BLUE=2,		/* COL_BLUE = 2*/
	COL_YELLOW=3, 		/* COL_YELLOW = 3*/
	COL_BLACK=4   		/* COL_BLACK = 4*/
	 };
```

*(11.6)*

```
enum COLORS{
	COL_WHITE=0,		/* COL_WHITE = 0*/
	COL_RED=10,		/* COL_RED = 10*/
	COL_BLUE,		/* COL_BLUE = 11*/
	COL_YELLOW, 		/* COL_YELLOW = 12*/
	COL_BLACK=100   	/* COL_BLACK = 100*/
	 };
```

Teraz przykład praktyczny. Bowiem zmienne wyliczeniowe można używać w instrukcji *if case* i wielu innych w których dopuszczone jest użycie zmiennej całkowitoliczbowej. Przyjrzyjmy się przykładom dwóch kodów realizujących ten sam problem.

*Przykład (11.7.1) kod z typem wyliczeniowym*


```
#include <stdio.h>

enum COLORS{COL_WHITE,COL_RED,COL_BLUE, COL_YELLOW, COL_BLACK };
enum BOOL{FALSE, TRUE};
struct rectangle
{
	float coordinates_x, coordinates_y;
	float height, width;
	enum COLORS color;
};
enum BOOL  it_is_yellow_rectangle(struct rectangle rectangle_object)
{
	if(rectangle_object.color==COL_YELLOW)
		return TRUE;
	else 
		return FALSE;
}

int main() 
{
	struct rectangle object_rectangle = {1, 1, 23, 43, COL_YELLOW};
	if(it_is_yellow_rectangle(object_rectangle)==TRUE)
		printf("Rectangle is YELLOW");	
	return 0;
}
```

*Przykład (11.7.2) kod bez typu wyliczeniowego*

```
#include <stdio.h>

struct rectangle
{
	float coordinates_x, coordinates_y;
	float height, width;
	int color;
};
int  it_is_yellow_rectangle(struct rectangle rectangle_object)
{
	if(rectangle_object.color==3)
		return 1;
	else 
		return 0;
}

int main() 
{
	struct rectangle object_rectangle = {1, 1, 23, 43, 3};
	if(it_is_yellow_rectangle(object_rectangle)==1)
		printf("Rectangle is YELLOW");	
	return 0;
}
```

*Wynik działania programów*

>Rectangle is YELLOW

A teraz pora określić który kod łatwiej przeczytać z poziomu programisty.

` `Prosta sprawa a pozwala nam uniknąć wielu pomyłek w kodzie. 
## **Definiowanie przy użyciu *typedef***
Narzędzie definiowane przez słowo kluczowe *typedef* daje nam kolejne możliwości. Pozwala ono zdefiniować nam identyfikator do własnego typu danych. Co za tym idzie możemy szybciej tworzyć zmienne zdefiniowanych przez nas typów *struct union* i *enum* (oraz tak naprawdę wszystkich typów danych. Pozwala on nam zdefiniować własne słowo kluczowe odpowiedzialne za typ danych. Jak można zauważyć w poniższym przykładzie (11.7) wszystkie zmienne złożone *struct* nie wymagają już zapisu „**struct** pkt” a wystarczy jedynie “punkt”. 

*Przykład (11.8.1) program z 11.1 z użyciem typedef*

```
#include <stdio.h>
#include <stdlib.h>

typedef struct pkt
{
	float x;
	float y;	
} punkt;

punkt wczytaj_punkt();
void wyswietl_punkt(punkt point);

int main() {
	punkt point = wczytaj_punkt(); 
	wyswietl_punkt(point);	
	return 0;
}

punkt wczytaj_punkt()
{
	punkt tmp;
	printf("Podaj wspolrzedna x: ");
	scanf(" %f", &tmp.x);
	printf("Podaj wspolrzedna y: ");
	scanf(" %f", &tmp.y);
	return tmp;
	
}

void wyswietl_punkt(punkt pkt)
{
	printf("(%5.2f,%5.2f)",pkt.x,pkt.y); 

}
```

*Przykład (11.8.2) program z 11.1 z użyciem typedef w inny sposób*

```
#include <stdio.h>
#include <stdlib.h>

struct pkt
{
	float x;
	float y;	
};
typedef struct pkt punkt;

punkt wczytaj_punkt();
void wyswietl_punkt(punkt point);

int main() {
	punkt point = wczytaj_punkt(); 
	wyswietl_punkt(point);	
	return 0;
}

punkt wczytaj_punkt()
{
	punkt tmp;
	printf("Podaj wspolrzedna x: ");
	scanf(" %f", &tmp.x);
	printf("Podaj wspolrzedna y: ");
	scanf(" %f", &tmp.y);
	return tmp;
	
}

void wyswietl_punkt(punkt pkt)
{
	printf("(%5.2f,%5.2f)",pkt.x,pkt.y); 
}
```

Analogicznie można definiować wszystkie poznane typy zmiennych (nawet te proste).

## **Zadania do samodzielnego wykonania**

Zdefiniuj strukturę punktu o całkowitych współrzędnych `x` i `y`. Wczytaj dwa punkty o współrzędnych od `-1000` do `1000` i oblicz ich odległość miejską: `|x1-x2| + |y1-y2|`. Wykorzystaj funkcję przyjmującą dwie struktury.

### Projekt: system ewidencji ligi piłkarskiej

System przechowuje piłkarzy, drużyny, mecze i jedną ligę. Piłkarz ma imię, nazwisko, wiek i kategorię wiekową. Drużyna ma nazwę, kategorię i listę swoich piłkarzy. Mecz łączy dwie drużyny; może być zaplanowany, rozegrany albo odwołany. Liga gromadzi drużyny z jednej kategorii oraz ich mecze.

Na potrzeby zadania przyjmij trzy kategorie: TRAMPKARZ (10–14 lat), JUNIOR (15–18 lat) i SENIOR (od 19 lat). Program ma obsługiwać najwyżej 20 piłkarzy, 4 drużyny i 6 meczów. W jednej drużynie może grać najwyżej 5 piłkarzy. Użyj tablic o stałym rozmiarze; nie jest tu potrzebna dynamiczna alokacja pamięci.

Wykonuj kolejne etapy, rozbudowując ten sam program:

1. Zdefiniuj typ wyliczeniowy kategorii wiekowych oraz struktury `pilkarz` i `druzyna`. Dodaj jednego piłkarza i jedną drużynę w kodzie, a następnie wypisz ich dane. Kategorię piłkarza ustalaj na podstawie wieku.
2. Zdefiniuj strukturę `mecz` i typ wyliczeniowy jego stanu: ZAPLANOWANY, ROZEGRANY, ODWOLANY. W strukturze użyj unii, która przechowuje albo wynik meczu (liczbę goli obu drużyn), albo powód odwołania. Stan meczu określa, które pole unii należy odczytać. Utwórz po jednym przykładzie meczu rozegranego i odwołanego, a następnie wypisz właściwe dane.
3. Dodaj menu do ewidencji piłkarzy: dodawanie, edycję i usuwanie. Nie przekraczaj limitu 20 osób. Piłkarza przypisanego do drużyny można usunąć dopiero po usunięciu go z tej drużyny.
4. Dodaj tworzenie drużyn oraz dopisywanie i usuwanie piłkarzy z drużyny. Piłkarz może należeć do jednej drużyny i musi mieć tę samą kategorię wiekową co ona. Nie przekraczaj limitu 4 drużyn ani 5 piłkarzy w każdej z nich.
5. Dodaj tworzenie meczu między dwiema różnymi drużynami, wpisanie jego wyniku oraz odwołanie z podaniem powodu. Po wpisaniu wyniku określ rezultat pierwszej drużyny za pomocą typu wyliczeniowego WYGRANA, PRZEGRANA, REMIS. Nie rozgrywaj ani nie odwołuj ponownie meczu, który ma już ustalony stan końcowy.
6. Zdefiniuj strukturę `liga` i utwórz ligę dla jednej wybranej kategorii. Mogą do niej należeć tylko drużyny z tej kategorii. Utwórz po jednym meczu dla każdej pary drużyn, bez powtórzeń; przy 4 drużynach będzie ich 6. Wylosuj kolejność tych meczów za pomocą `rand()` z `<stdlib.h>`. Wyświetl listę meczów oraz wyniki rozegranych spotkań.

W gotowym systemie użytkownik powinien móc kolejno dodać piłkarzy i drużyny, przypisać piłkarzy do drużyn, utworzyć ligę, wygenerować mecze, rozstrzygnąć albo odwołać każdy mecz oraz obejrzeć terminarz i wyniki. Przy każdej operacji sprawdzaj limity tablic i zgodność kategorii wiekowych.

***
[Poprzednia część](https://github.com/CyberMALab/Tablice-znakow.git) | [Spis treści](https://github.com/CyberMALab/Wprowadzenie-do-programowania-w-j-zyku-ANSI-C.git) | [Następna część](https://github.com/CyberMALab/Wprowadzenie-do-wskaznikow.git)
***
&copy; Cyberspace Modelling and Analysis Laboratory
