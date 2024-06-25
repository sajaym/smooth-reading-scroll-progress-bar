# Smooth Reading Scroll Progress Bar

A customizable scroll progress bar library that enhances UX by visually indicating scroll position. Smoothly fills up during scrolling and fades out when reaching the middle of the content. Lightweight, easy to integrate, and ensures a non-intrusive navigation experience.



## Usage

1. Add the necessary CSS styles to your `styles.css` file:

   ```css
   .progress-container {
       position: fixed;
       top: 0;
       width: 100%;
       height: 4px;
       background: #f1f1f1;
       z-index: 100;
       transition: opacity 0.3s ease-in-out;
   }

   .progress-bar {
       height: 100%;
       background: #4CAF50;
       width: 0%;
       transition: width 0.2s ease-in-out;
   }
   ```

2. Add the necessary JavaScript code to your `script.js` file:
    ```javascript
    // Get the progress bar and progress container elements
    const progressBar = document.getElementById('progressBar');
    const progressContainer = document.querySelector('.progress-container');
    
    // Get the main content section element
    const main = document.querySelector('main');
    
    // Add scroll event listener to the window
    window.addEventListener('scroll', () => {
        // Get the current scroll position
        const winScroll = document.body.scrollTop || document.documentElement.scrollTop;
        
        // Calculate the total height of the main content section
        const height = main.scrollHeight - document.documentElement.clientHeight;
        
        // Calculate the percentage of the page scrolled
        const scrolled = (winScroll / height) * 100;
    
        // Update the width of the progress bar based on the scroll percentage
        progressBar.style.width = `${scrolled}%`;
    
        // Calculate the position of the bottom of the main content section
        const mainBottom = main.offsetTop + main.offsetHeight;
        
        // Calculate the middle position of the viewport
        const viewportMiddle = window.innerHeight / 2;
    
        // Check if the bottom of the main content section is above or at the middle of the viewport
        if (mainBottom - viewportMiddle <= winScroll) {
            // If true, hide the progress bar by setting its opacity to 0
            progressContainer.style.opacity = '0';
        } else {
            // If false, show the progress bar by setting its opacity to 1
            progressContainer.style.opacity = '1';
        }
    });
    ```

3. Add the necessary HTML elements to your page:

   ```html
   <div class="progress-container">
       <div class="progress-bar" id="progressBar"></div>
   </div>
   ```

   - A container element with the class `progress-container`
   - A progress bar element with the ID `progressBar` inside the container
   - A `main` element wrapping your main content

