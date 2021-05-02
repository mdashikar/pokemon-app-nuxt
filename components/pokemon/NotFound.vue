<template>
  <div class="py-8">
    <div class="mx-auto p-2 lg:w-1/3 md:w-1/2 w-full cursor-pointer">
      <div
        class="h-full flex items-center border-gray-200 border p-4 rounded-lg"
      >
        <div class="flex-grow">
          <h2 class="text-gray-900 title-font font-medium capitalize">
            {{ text }}
          </h2>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'NotFound',
  props: {
    text: { type: String, default: 'Not found.' },
  },
}
</script>
