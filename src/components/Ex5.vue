<script setup>
import axios from 'axios';
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const moods = ref(['Happy', 'Sad', 'Angry']);
const subject = ref('');
const entry = ref('');
const mood = ref('');

const router = useRouter();

// Add Code Here
async function submitPost() {
  try {
    const response = await axios.post('http://localhost:8000/posts', {
      subject: subject.value,
      entry: entry.value,
      mood: mood.value
    });
    console.log('Post created:', response.data);

    // clear the form
    subject.value = '';
    entry.value = '';
    mood.value = '';

    // optionally go back to the main page
    router.push('/ViewPosts/');
  } catch (error) {
    console.error('Error creating post:', error);
  }
}
</script>

<template>
    <div class="table m-2">
        <h3>Add a New Blog Post</h3>

        Subject: <input type='text' size='30' v-model='subject' required>
        <br>

        Entry: <br>
        <textarea name='entry' cols='80' rows='5' v-model='entry' required></textarea>
        <br>

        Mood:
        <!-- TODO: Build a dropdown list here for selecting the mood -->
        <select v-model='mood'>
            <option value='' disabled>-- Select a mood --</option>
            <option v-for='m in moods' :key='m' :value='m'>{{ m }}</option>
        </select>
        <br>

        <br>
        <button @click='submitPost'>Submit New Post</button>

        <hr>
        <RouterLink to="/ViewPosts/">Click here to return to Main Page</RouterLink>  
    </div>
</template>

