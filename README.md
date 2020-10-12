using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;

namespace LAB3
{
    class Car
    {
        private string Name;
        private int Seats;
        private int Gas;

        public Car(string Name, int Seats, int Gas)
        {
            this.Name = Name;
            this.Seats = Seats;
            this.Gas = Gas;
        }

        public string GetName() { return Name; }
        public int GetSeats() { return Seats; }
        public int GetGas() { return Gas; }
    }
    class Program
    {
        static void Main(string[] args)
        {
            const int Cn = 100;
            Car[] C1 = new Car[Cn];
            Car[] C2 = new Car[Cn];
            const string Cfd = "C:\\Users\\guodu\\Documents\\Guodos\\KTU\\Programavimas\\LAB3\\LAB3\\duom.txt";
            const string Cfdd = "C:\\Users\\guodu\\Documents\\Guodos\\KTU\\Programavimas\\LAB3\\LAB3\\duom2.txt";
            const string Cfr = "C:\\Users\\guodu\\Documents\\Guodos\\KTU\\Programavimas\\LAB3\\LAB3\\rez.txt";
            int n1,n2;
            string Who1, Who2;
            Fileread(Cfd, C1, out n1, out Who1);
            Fileread(Cfdd, C2, out n2, out Who2);
            using (var fr = File.AppendText(Cfr))
            {
                    fr.WriteLine("Talpiausias studento {0} automobilis, sedimos vietos: {1} ", Who1, C1[MostSeats(C1, n1)].GetSeats());
                    fr.WriteLine("Talpiausias studento {0} automobilis , sedimos vietos: {1} ", Who2, C2[MostSeats(C2, n2)].GetSeats());
            }
        }
        static void Fileread(string fd, Car[] C, out int n, out string Who)
        {
            n = 0;
            using (StreamReader reader = new StreamReader(fd))
            {
                string line=reader.ReadLine();
                Who = line;
                while ((line = reader.ReadLine()) != null)
                {
                    n++;
                    string[] parts = line.Split(' ');
                    string Name = parts[0];
                    int Seats = int.Parse(parts[1]);
                    int Gas = int.Parse(parts[2]);
                    C[n] = new Car(Name, Seats, Gas);
                }
            }
        }
        static int MostSeats(Car[] C, int n)
        {
            int k = 0;
            for (int i = 0; i < n; i++) 
                if (C[i].GetSeats() < C[k].GetSeats())
                    k = i;
         return k;
        }
    }
}
