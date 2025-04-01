<template>
  <div class="container mx-auto px-6 py-8">
    <h1 class="text-4xl font-bold mb-6">Contact Us</h1>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
      <div class="bg-white p-6 rounded-lg shadow-md">
        <h2 class="text-2xl font-semibold mb-4">Get in Touch</h2>
        <form class="space-y-4">
          <div>
            <label class="block text-gray-700 mb-2" for="name">Name</label>
            <input type="text" id="name" class="w-full p-2 border rounded-md" />
          </div>
          <div>
            <label class="block text-gray-700 mb-2" for="email">Email</label>
            <input type="email" id="email" class="w-full p-2 border rounded-md" />
          </div>
          <div>
            <label class="block text-gray-700 mb-2" for="message">Message</label>
            <textarea id="message" rows="4" class="w-full p-2 border rounded-md"></textarea>
          </div>
          <button type="submit" class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600">
            Send Message
          </button>
        </form>
      </div>
      <div>
        <h2 class="text-2xl font-semibold mb-4">Contact Information</h2>
        <div class="space-y-4">
          <div>
            <h3 class="font-semibold">Address</h3>
            <p class="text-gray-600">123 Business Street<br />City, State 12345</p>
          </div>
          <div>
            <h3 class="font-semibold">Email</h3>
            <p class="text-gray-600">info@example.com</p>
          </div>
          <div>
            <h3 class="font-semibold">Phone</h3>
            <p class="text-gray-600">(123) 456-7890</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>