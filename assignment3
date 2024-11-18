import java.util.*;
import java.util.concurrent.TimeUnit;

public class ArraySorting {

    public static void main(String[] args) {
        int[] sizes = {50, 500, 1000, 2000, 5000, 10000};
        int cutoff[] = {10, 50, 200};

        for (int size : sizes) {
            int[] array = generateRandomArray(size);
            System.out.println("Array Size: " + size);

            // Insertion Sort
            int[] copy = array.clone();
            long start = System.nanoTime();
            insertionSort(copy);
            long end = System.nanoTime();
            System.out.println("Insertion Sort: " + (end - start) + " ns");

            // Heap Sort
            copy = array.clone();
            start = System.nanoTime();
            heapSort(copy);
            end = System.nanoTime();
            System.out.println("Heap Sort: " + (end - start) + " ns");

            // Merge Sort
            copy = array.clone();
            start = System.nanoTime();
            mergeSort(copy);
            end = System.nanoTime();
            System.out.println("Merge Sort: " + (end - start) + " ns");

            // Quick Sort without CUTOFF
            copy = array.clone();
            start = System.nanoTime();
            quickSort(copy, 0, copy.length - 1, 0);
            end = System.nanoTime();
            System.out.println("Quick Sort (No Cutoff): " + (end - start) + " ns");

            // Quick Sort with CUTOFF
            for (int c : cutoff) {
                copy = array.clone();
                start = System.nanoTime();
                quickSort(copy, 0, copy.length - 1, c);
                end = System.nanoTime();
                System.out.println("Quick Sort (Cutoff=" + c + "): " + (end - start) + " ns");
            }
        }
    }

    // Generate random integer array
    public static int[] generateRandomArray(int size) {
        Random rand = new Random();
        int[] array = new int[size];
        for (int i = 0; i < size; i++) {
            array[i] = rand.nextInt(10000); // Random numbers in range [0, 9999]
        }
        return array;
    }

    // Insertion Sort
    public static void insertionSort(int[] array) {
        for (int i = 1; i < array.length; i++) {
            int key = array[i];
            int j = i - 1;
            while (j >= 0 && array[j] > key) {
                array[j + 1] = array[j];
                j--;
            }
            array[j + 1] = key;
        }
    }

    // Heap Sort
    public static void heapSort(int[] array) {
        int n = array.length;
        for (int i = n / 2 - 1; i >= 0; i--)
            heapify(array, n, i);
        for (int i = n - 1; i > 0; i--) {
            int temp = array[0];
            array[0] = array[i];
            array[i] = temp;
            heapify(array, i, 0);
        }
    }

    private static void heapify(int[] array, int n, int i) {
        int largest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        if (left < n && array[left] > array[largest])
            largest = left;
        if (right < n && array[right] > array[largest])
            largest = right;
        if (largest != i) {
            int swap = array[i];
            array[i] = array[largest];
            array[largest] = swap;
            heapify(array, n, largest);
        }
    }

    // Merge Sort
    public static void mergeSort(int[] array) {
        if (array.length > 1) {
            int mid = array.length / 2;
            int[] left = Arrays.copyOfRange(array, 0, mid);
            int[] right = Arrays.copyOfRange(array, mid, array.length);
            mergeSort(left);
            mergeSort(right);
            merge(array, left, right);
        }
    }

    private static void merge(int[] array, int[] left, int[] right) {
        int i = 0, j = 0, k = 0;
        while (i < left.length && j < right.length) {
            if (left[i] <= right[j]) {
                array[k++] = left[i++];
            } else {
                array[k++] = right[j++];
            }
        }
        while (i < left.length) {
            array[k++] = left[i++];
        }
        while (j < right.length) {
            array[k++] = right[j++];
        }
    }

    // Quick Sort
    public static void quickSort(int[] array, int low, int high, int cutoff) {
        if (low < high) {
            if (high - low <= cutoff) {
                insertionSort(Arrays.copyOfRange(array, low, high + 1));
            } else {
                int pi = partition(array, low, high);
                quickSort(array, low, pi - 1, cutoff);
                quickSort(array, pi + 1, high, cutoff);
            }
        }
    }

    private static int partition(int[] array, int low, int high) {
        int pivot = array[high];
        int i = (low - 1);
        for (int j = low; j < high; j++) {
            if (array[j] < pivot) {
                i++;
                int temp = array[i];
                array[i] = array[j];
                array[j] = temp;
            }
        }
        int temp = array[i + 1];
        array[i + 1] = array[high];
        array[high] = temp;
        return i + 1;
    }
}
