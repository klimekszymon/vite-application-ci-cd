<script setup lang="ts">
import { ref , onMounted} from 'vue';
import type { Ref } from 'vue';
// Initialize the books array with the Library type
const books: Ref<Book[]> = ref([]);
const newBook = ref({
  title: '',
  author: '',
  year: 0,
})

const mockBooks: Book[] = [
  {
    title: "Mock Book 1",
    author: "Mock Author 1",
    year: 2021,
  },
  {
    title: "Mock Book 2",
    author: "Mock Author 2",
    year: 2022,
  },
  {
    title: "Mock Book 3",
    author: "Mock Author 3",
    year: 2023,
  },
  {
    title: "Mock Book 4",
    author: "Mock Author 4",
    year: 2024,
  },
  {
    title: "Mock Book 5",
    author: "Mock Author 5",
    year: 2025,
  },
];

// Initialize the books array with the mock data
books.value = mockBooks;
type Book = {
  title: string;
  author: string;
  year: number;
};

// Define the type for the array of books
// type Library = Book[];



// Function to add a book to the library
const addBook = (book: Book) => {
  books.value.push(book);
  saveLibraryToLocalStorage();
};

// Function to remove a book from the library
const removeBook = (index: number) => {
  books.value.splice(index, 1);
  saveLibraryToLocalStorage();
};

// Function to save the library to local storage
const saveLibraryToLocalStorage = () => {
  localStorage.setItem('library', JSON.stringify(books.value));
};

// Function to load the library from local storage
const loadLibraryFromLocalStorage = () => {
  const libraryData = localStorage.getItem('library');
  if (libraryData) {
    books.value = JSON.parse(libraryData);
  }
};

// Load the library from local storage when the component is mounted
onMounted(() => {
  loadLibraryFromLocalStorage();
});
</script>

<template>
  <br />
  <h1 class="text-3xl font-bold mb-4 mt-12">Testing Library</h1>
  <form class="mt-4">
    <div class="grid grid-cols-4 gap-x-4 m-2 p-4 bg-gray-400 ">
      <input type="text" v-model="newBook.title" placeholder="Title"  class="rounded-md shadow-md p-4" />
      <input type="text" v-model="newBook.author" placeholder="Author"  class="rounded-md shadow-md p-4" />
      <input type="number" v-model="newBook.year" placeholder="Year"  class="rounded-md shadow-md p-4" />
      <button @click="addBook(newBook)" class="px-4 py-2 bg-green-700 text-white rounded">Add Book</button>
    </div>
  </form>
  <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-0">
    <div v-for="(book, index) in books" :key="index" class="bg-black p-4 m-2 rounded shadow inline">
      <p class="text-xl font-bold">{{ book.title.toUpperCase() }}</p>
      <hr class="my-2 p-1 bg-green-900" />
      <p class="text-lg">Author: {{ book.author }}</p>
      <p class="text-lg">Year: {{ book.year }}</p>
      <button @click="removeBook(index)" class="px-4 py-2 mt-2 bg-red-500 text-white rounded">Remove</button>
    </div>
  </div>
</template>
