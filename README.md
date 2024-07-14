# Squarespace Dynamic Opening Times Component

This component allows you to dynamically display opening times on your Squarespace website, showing only the opening times of the current day with a button to show all opening times, and highlighting the current day in the opened state.

## Instructions

1. Make a code block wherever you want your Opening Times displayed.
2. Copy and insert the HTML and CSS into the desired location.
3. Go to your Code Injection and copy the JavaScript into the Footer Code.
4. Customize the opening times as needed.

## Example

Here is an example of the opening times component in action:

![Opening Times Example](https://i.postimg.cc/CMnykSJg/ezgif-com-animated-gif-maker.gif)

## CodeBlock

```html
<!-- Hidden Container -->
<div id="all-opening-times" style="display: none;">
  <div data-day="0">Sonntag<br>14:00–22:00</div>
  <div data-day="1">Montag<br>13:00–22:00</div>
  <div data-day="2">Dienstag<br>Geschlossen</div>
  <div data-day="3">Mittwoch<br>13:00–22:00</div>
  <div data-day="4">Donnerstag<br>13:00–22:00</div>
  <div data-day="5">Freitag<br>13:00–22:00</div>
  <div data-day="6">Samstag<br>15:00–22:00</div>
</div>

<!-- Visible Container -->
<div id="dynamic-opening-times" style="text-align: center;">
</div>

<!-- Button to Show All Opening Times -->
<div id="toggle-opening-times" class="toggle-container">
  <a href="javascript:void(0)" id="show-all-times" class="toggle-link">Öffnungszeiten anzeigen</a>
</div>

<style>
  .toggle-container {
    text-align: center;
    margin-top: 10px;
  }

  .toggle-link {
    font-size: 16px;
    color: #FF4500;
    text-decoration: none;
  }

  .toggle-link:hover {
    text-decoration: underline;
  }

  #all-opening-times {
    text-align: center;
  }

  #all-opening-times div {
    text-align: center;
    margin: 0 auto;
    display: block;
  }

  .highlight-today {
    color: #e1843a;
    font-weight: bold;
  }

  @media (max-width: 600px) {
    .toggle-link {
      font-size: 14px;
    }
  }
</style>


Footer Script

<script>
document.addEventListener('DOMContentLoaded', function() {
  // Dynamic Opening Times Script
  var today = new Date().getDay();
  var todayOpeningTime = document.querySelector('#all-opening-times div[data-day="' + today + '"]').cloneNode(true);
  var dynamicOpeningTimesContainer = document.querySelector('#dynamic-opening-times');
  dynamicOpeningTimesContainer.appendChild(todayOpeningTime);

  var showAllTimesLink = document.getElementById('show-all-times');
  var allOpeningTimes = document.getElementById('all-opening-times');
  var isAllTimesVisible = false;

  showAllTimesLink.addEventListener('click', function() {
    if (isAllTimesVisible) {
      allOpeningTimes.style.display = 'none';
      showAllTimesLink.textContent = 'Öffnungszeiten anzeigen';
      dynamicOpeningTimesContainer.style.display = 'block';
    } else {
      allOpeningTimes.style.display = 'block';
      showAllTimesLink.textContent = 'Öffnungszeiten verbergen';
      dynamicOpeningTimesContainer.style.display = 'none';
      // Highlight the current day in the full list
      var fullTodayOpeningTime = document.querySelector('#all-opening-times div[data-day="' + today + '"]');
      fullTodayOpeningTime.classList.add('highlight-today');
    }
    isAllTimesVisible = !isAllTimesVisible;
  });
});
</script>
