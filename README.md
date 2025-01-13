```csharp
﻿using System;

namespace LinkedList
{
    //LinkedList düğümü
    class Node 
    {
        public int Data; //Verilerin tutulacağı değişken.
        public Node Next; //Sonraki veriye referans.
    }

    //LinkedList sınıfı
    class LinkedList
    {
        public Node Head; //ilk Node

        //Listeye veri ekleyen metod.
        public void AddList(int data)
        {
            Node newNode = new Node { Data = data, Next = null };  //Next ilk başta null olur.

            if (Head == null) //Head boş ise
            { 
                Head = newNode; //newNode değişkeni Head değişkenine atanır.
            }
            else
            {
                Node temp = Head; //temp adında yeni bir değişken oluşturulur. Bu değişkeni tüm listeyi kontrol etmede kullanırız.

                while (temp.Next != null) //temp.Next değişkeni null değil ise döngüyü çalıştır.
                {
                    temp = temp.Next; //Sonraki Node'a geç.
                }
                temp.Next = newNode; //temp.Next sonraki newNode değişkenine aktarılır ve Next listeye yeni veri eklenene kadar yine null olur.
            }
        }

        //Listedeki verileri ekrana yazdıran metod
        public void PrintList()
        {
            Node temp = Head; //temp adında tüm listeyi gezecek bir değişken oluşturup Head ona aktardık.

            while (temp != null) //temp boş değilse döngüyü çalıştır.
            {
                Console.WriteLine(temp.Data); //temp.Data ekrana yazdırılır.
                temp = temp.Next; //Sonraki düğüme geç.
            }
        }

        //Listeden veri silme metodu
        public void Delete(int data)
        {
            if (Head == null) //Head boş ise
            {
                Console.WriteLine("Liste boş.");
                return; //Hata yazdırılır ve return edilir.
            }

            if (Head.Data == data) //Eğer Head.Data (ilk Node) girdiğimiz değere eşitse 
            {
                Head = Head.Next; //Sonraki düğüme geçer ve ilk değeri siler.
                return;
            }
            
            Node temp = Head; //Yine tüm listeyi dolaşması için temp adındaki değişkeni oluşturup Head'i ona atıyoruz.

            while (temp.Next != null && temp.Next.Data != data) //temp.Next boş değilse ve temp.Next.Data ise data'ya eşit değilse
            {
                temp = temp.Next; //silinecek değer bulunana kadar temp.Next'i temp'e aktarır.
            }

            if (temp.Next != null) //Döngüdeki koşul sağlandıysa
            {
                temp.Next = temp.Next.Next; //bir sonraki veriyi önceki veriye aktararak o veriyi siler.
            }
            else //Döngüdeki koşul sağlanmamışsa
            {
                Console.WriteLine("Listede böyle bir değer yok."); //Ekranda bu hata yazdırılır.
            }
        }

        //Listede veri arama metodu
        public void Search(int data)
        {
            if (Head == null) //Head (ilk Node) boş ise
            {
                Console.WriteLine("Liste boş");
                return; //hata ekrana yazdırılır.
            }

            if (Head.Data == data) //Eğer Head.Data'daki veri girdiğimiz değer "data"ya eşitse
            {
                Console.WriteLine($"Aradığınız veri \"{Head.Data}\" bulundu");
                return; //bulunan veri ekrana yazdırılır.
            }

            Node temp = Head; //Yine tüm listeyi dolaşması için temp adındaki değişkeni oluşturup Head'i ona atıyoruz.

            while (temp.Next != null) //temp.Next boş değil ise
            {
                temp = temp.Next; //aranan veriyi bulana kadar sonraki veriye geçer ve döngüyü devam ettirir.
            }

            if (temp.Data == data) //eğer koşul sağlanmışsa
            {
                Console.WriteLine($"Aradığınız veri \"{temp.Data}\" bulundu"); //ekrana bulunan değer yazdırılır.
            }
            else //koşul sağlanmamışsa
            {
                Console.WriteLine("Listede böyle bir değer yok."); //ekrana hata yazdırılır.
            }
        }
    }

    class Program
    {
        static void Main()
        {
            LinkedList linkedList = new LinkedList(); //LinkedList sınıfının bir örneğini (instance) oluşturuyoruz.
            
            linkedList.AddList(5); //Listeye eleman(5) eklendi.
            linkedList.AddList(10);
            linkedList.AddList(15);
            linkedList.AddList(20);
            linkedList.AddList(25);
            linkedList.PrintList(); //Tüm elemanlar ekranda yazdırılır.
            Console.WriteLine("-------------------");
            linkedList.Delete(15); //Listeden eleman(15) silinir.
            linkedList.PrintList();
            Console.WriteLine("-------------------");
            linkedList.Search(25); //Listede eleman(25) aranır.
            linkedList.Search(15); //Listede daha önce sildiğimiz eleman(15) aranacak ama olmadığı için hata ekrana yazdırılacak.
            Console.ReadKey();
        }
    }
}
```
