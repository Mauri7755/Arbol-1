# Arbol-1

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace PrimerArbol
{
    class Arbol1
    {
        public class Nodo
        {
            private int Datos;
            private Nodo Izquierdo, Derecho;

            public Nodo(int Datos, Nodo izq, Nodo der)
            {
                this.Datos = Datos;
                this.Izquierdo = izq;
                this.Derecho = der;
            }

            public virtual int Dato
            {
                get
                {
                    return Datos;
                }
                set
                {
                    this.Datos = value;
                }
            }

            //Ramas izquierdas
            public virtual Nodo Izquierdo1
            {
                get
                {
                    return Izquierdo;
                }
                set
                {
                    this.Izquierdo = value;
                }
            }

            //Ramas derechas
            public virtual Nodo Derecho1
            {
                get
                {
                    return Derecho;
                }
                set
                {
                    this.Derecho = value;
                }
            }


        }

        public class ArbolBinary
        {

            private Nodo Raiz;
            internal int cant;
            internal int Altura;

            public ArbolBinary()
            {
                this.Raiz = null;
            }
            //Metodos que agregan los datos
            public virtual void Agregar(int Datos)
            {
                Nodo nuevo = new Nodo(Datos, null, null);
                Insert(nuevo, Raiz);
            }

            public virtual void Insert(Nodo nuevo, Nodo pivote)
            {
                if (this.Raiz == null)
                {
                    Raiz = nuevo;
                }
                else
                {
                    if (nuevo.Dato <= pivote.Dato)
                    {
                        if (pivote.Izquierdo1 == null)
                        {
                            pivote.Izquierdo1 = nuevo;
                        }
                        else
                        {
                            Insert(nuevo, pivote.Izquierdo1);
                        }
                    }
                    else
                    {
                        if (pivote.Derecho1 == null)
                        {
                            pivote.Derecho1 = nuevo;
                        }
                        else
                        {
                            Insert(nuevo, pivote.Derecho1);
                        }
                    }
                }
            }
            //Nodos
            public virtual bool Exist(int info)
            {
                Nodo Reco = Raiz;
                while (Reco != null)
                {
                    if (info == Reco.Dato)
                    {
                        return true;
                    }
                    else if (info > Reco.Dato)
                    {
                        Reco = Reco.Derecho1;
                    }
                    else
                    {
                        Reco = Reco.Izquierdo1;
                    }
                }
                return false;
            }

            public virtual int Cantidad()
            {
                cant = 0;
                Cantidad(Raiz);
                return cant;
            }
            //Metodos de las hojas
            private void Cantidad(Nodo Reco)
            {
                if (Reco != null)
                {
                    cant++;
                    Cantidad(Reco.Izquierdo1);
                    Cantidad(Reco.Derecho1);
                }
            }

            private void CantidadNodosLeaf(Nodo Reco)
            {
                if (Reco != null)
                {
                    if (Reco.Izquierdo1 == null && Reco.Derecho1 == null)
                    {
                        cant++;
                    }
                    CantidadNodosLeaf(Reco.Izquierdo1);
                    CantidadNodosLeaf(Reco.Derecho1);
                }
            }

            public virtual int CantidadNodosLeaf()
            {
                cant = 0;
                CantidadNodosLeaf(Raiz);
                return cant;
            }
            //Metodos de como obtener la Altura
            public virtual int ReturnAltura()
            {
                Altura = 0;
                ReturnAltura(Raiz, 1);
                return Altura;
            }
            private void ReturnAltura(Nodo Reco, int Nivel)
            {
                if (Reco != null)
                {
                    ReturnAltura(Reco.Izquierdo1, Nivel + 1);
                    if (Nivel > Altura)
                    {
                        Altura = Nivel;
                    }
                    ReturnAltura(Reco.Derecho1, Nivel + 1);
                }
            }
            internal string[] Niveles;
            public virtual int AlturaArbol()
            {
                Altura = 0;
                AlturaArbol(Raiz, 0);
                return Altura;
            }
            private void AlturaArbol(Nodo pivote, int Nivel)
            {
                if (pivote != null)
                {
                    AlturaArbol(pivote.Izquierdo1, Nivel + 1);
                    if (Nivel > Altura)
                    {
                        Altura = Nivel;
                    }
                    AlturaArbol(pivote.Derecho1, Nivel + 1);
                }
            }
            //Metodos de el nivel
            public virtual void PrintNivel()
            {
                Niveles = new string[Altura + 1]; 

                PrintNivel(Raiz, 0);
                for (int i = 0; i < Niveles.Length; i++)
                {
                    Console.WriteLine(Niveles[i] + " En nivel: " + i);
                }
            }
            public virtual void PrintNivel(Nodo pivote, int lvl)
            {
                if (pivote != null)
                {
                    Niveles[lvl] = pivote.Dato + ", " + ((!string.ReferenceEquals(Niveles[lvl], null)) ? Niveles[lvl] : "");
                    PrintNivel(pivote.Derecho1, lvl + 1);
                    PrintNivel(pivote.Izquierdo1, lvl + 1);
                }
            }
            public virtual void PrintAlturaDeCadaNod()
            {
                PrintAlturaDeCadaNod(Raiz, 1);
            }
            private void PrintAlturaDeCadaNod(Nodo reco, int nivel)
            {
                if (reco != null)
                {
                    Console.WriteLine("Nodo contiene: " + reco.Dato + " y su Altura es: " + nivel);
                    PrintAlturaDeCadaNod(reco.Izquierdo1, nivel + 1);
                    PrintAlturaDeCadaNod(reco.Derecho1, nivel + 1);
                }
            }
        }
        static void Main(string[] args)
        {
            ArbolBinary Obj = new ArbolBinary();
            int ob;
            int a = 55, b = 14, c = 74, d = 32, e = 40, f = 7;
            Console.WriteLine(" Insertando valores manualmente en el árbol: ");
            Obj.Agregar(a);
            Obj.Agregar(b);
            Obj.Agregar(c);
            Obj.Agregar(d);
            Obj.Agregar(e);
            Obj.Agregar(f);
            //Obj.Agregar(g = y.Next(1, 99));
            Console.WriteLine(" " + "/" + "f");
            Console.WriteLine("e" + " " + " " + "/" + "d");
            Console.WriteLine(" " + "|" + "a" + " " + "--" + "c");
            Console.WriteLine(" " + " " + " " + "|" + "b");

            Console.WriteLine("Valores insertados: " + a + " " + b + " " + c + " " + d + " " + e + " " + f + " ");
            Obj.PrintAlturaDeCadaNod();
            do
            {
                Console.WriteLine(" ");
                Console.WriteLine(" ");
                Console.WriteLine("1.-Cantidad de nodos del arbol.");
                Console.WriteLine("2.-Cantidad de nodos hoja.");
                Console.WriteLine("3.-Altura del arbol.");
                Console.WriteLine("0.-Salir");
                ob = int.Parse(Console.ReadLine());
                switch (ob)
                {
                    case 1:
                        Console.WriteLine("Cantidad de nodos del árbol:" + Obj.Cantidad());
                        break;
                    case 2:
                        Console.WriteLine("Cantidad de nodos hoja:" + Obj.CantidadNodosLeaf());
                        break;
                    case 3:
                        Console.WriteLine("La Altura del arbol es:" + Obj.ReturnAltura());
                        break;
                }
            } while (ob != 0);
            Console.ReadKey();
        }
    }
}

