<template>
    <div>
        <div class="about-section">
            <h1>About Us</h1>
            <p>Some text about who we are and what we do.</p>
            <p>Build this assigment with a lot of work, but evantually we did it.</p>
        </div>

        <h2 style="text-align:center">Our Team</h2>
        <div class="row">
        <div class="column">
            <div class="card">
            <img src="../assets/ni.jpeg" alt="Jane" style="width:100%">
            <div class="container">
                <h2>Nir Cohen</h2>
                <p class="title">CEO & Founder</p>
                <p>CEO, founder and creator of this page and many others.</p>
                <p>nirai@post.bgu.ac.il</p>
                <p><button class="button">Contact</button></p>
            </div>
            </div>
        </div>

        <div class="column">
            <div class="card">
            <img src="../assets/sha.jpeg" alt="Mike" style="width:100%">
            <div class="container">
                <h2>Shahar Adam</h2>
                <p class="title">Art Director & Designer</p>
                <p>Some text that describes me lorem ipsum ipsum lorem.</p>
                <p>mike@example.com</p>
                <p><button class="button">Contact</button></p>
            </div>
            </div>
        </div>

        <div class="column">
            <div class="card">
            <img src="../assets/ca.jpeg" alt="John" style="width:100%">
            <div class="container">
                <h2>Rio The Cat</h2>
                <p class="title">Emotional Support</p>
                <p>Cause many problems but we can't fire him.</p>
                <p>Rio@gmail.com</p>
                <p><button class="button">Contact</button></p>
            </div>
        </div>
        </div>
        </div>
    </div>
</template>

<script>

</script>

<style>
body {
  font-family: Arial, Helvetica, sans-serif;
  margin: 0;
}

html {
  box-sizing: border-box;
}

*, *:before, *:after {
  box-sizing: inherit;
}

.column {
  float: left;
  width: 33.3%;
  margin-bottom: 16px;
  padding: 0 8px;
}

.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  margin: 8px;
  width: 500px;
}

.about-section {
  padding: 50px;
  text-align: center;
  background-color: #474e5d;
  color: white;
}

.container {
  padding: 0 16px;
}

.container::after, .row::after {
  content: "";
  clear: both;
  display: table;
}

.title {
  color: grey;
}

.button {
  border: none;
  outline: 0;
  display: inline-block;
  padding: 8px;
  color: white;
  background-color: #000;
  text-align: center;
  cursor: pointer;
  width: 100%;
}

.button:hover {
  background-color: #555;
}

@media screen and (max-width: 650px) {
  .column {
    width: 100%;
    display: block;
  }
}
img {
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 5px;
  width: 10px;
}

</style>
