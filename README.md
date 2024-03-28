using System;
using System.Diagnostics;

class Program
{
    static int BinarySearchIterative(int[] array, int target)
    {
        int left = 0;
        int right = array.Length - 1;

        while (left <= right)
        {
            int mid = left + (right - left) / 2;

            if (array[mid] == target)
                return mid;
            else if (array[mid] < target)
                left = mid + 1;
            else
                right = mid - 1;
        }

        return -1;
    }

    static int BinarySearchRecursive(int[] array, int target, int left, int right)
    {
        if (left > right)
            return -1;

        int mid = left + (right - left) / 2;

        if (array[mid] == target)
            return mid;
        else if (array[mid] < target)
            return BinarySearchRecursive(array, target, mid + 1, right);
        else
            return BinarySearchRecursive(array, target, left, mid - 1);
    }

    static void Main()
    {
        int[] array = new int[10000000];

        for (int i = 0; i < array.Length; i++)
        {
            array[i] = i;
        }

        int target = 9999999;

        Stopwatch sw = new Stopwatch();

        // Измеряем время выполнения итеративного алгоритма
        sw.Start();
        int resultIterative = BinarySearchIterative(array, target);
        sw.Stop();
        Console.WriteLine($"Iterative search time: {sw.Elapsed}");

        // Измеряем время выполнения рекурсивного алгоритма
        sw.Reset()
