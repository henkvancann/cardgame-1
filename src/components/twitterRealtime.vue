<template>
<div id="slide-menu-and-buttons-wrapper">
    <div class="slide-menu-wrapper">
        <Typewriter />
        <div class="twitter-open-close-handle"></div>
        <div class="content container-fluid pt-0">
            <!-- BEGIN own content -->
            <div class="tweets-container row m-0 p-0">
                <h1 class="visuallyhidden">Tweets</h1>
                <!-- <button class="button-open-close-tweets-container"><span class="visuallyhidden">Open / close tweetstream</span></button> -->

                <!-- REALTIME TWEETS -->
                <div class="tweets-realtime col-md-12 m-0 p-0" style="padding-bottom: 10em !important;">
                    <nav class="navbar navbar-expand-md sticky-top p-0 " style="background: #1FA1F2;">
                        <div class="row m-0 p-0" style="width: 100%;">
                            <div class="col-md-12 m-0 p-0 ">
                                <!-- START STOP -->
                                <TwitterRealTimeStartStopToggle class="align-middle inline mr-2" style="width: 20px; height: 20px;transform: translateY(-0.1em);" />

                                <!-- CONFIGURATION -->
                                <button type="button" class="tweet-stream-configuration btn btn-outline-dark align-middle inline ml-0" style="border: none;" data-toggle="modal" data-target="#tweetStreamConfigurationModal">
                                    <span class="visuallyhidden">Tweetstream configuration</span>
                                    <img style="width: 20px;" src="@/assets/img/icons/ui/configuration.svg" alt="" />
                                </button>

                                <!-- ALL TWEETS -->
                                <!-- <div class="form-check ml-0 m-0 " style="display: inline;">
                                    <input type="checkbox" class="form-check-input mt-3" id="showAllTweets">
                                    <label style="color: #eee;" class="form-check-label align-middle inline" for="showAllTweets">all tweets</label>
                                </div> -->

                                <!-- CLEAR -->
                                <button class="btn btn-sm btn-outline-light ml-0 clear-tweet-stream-button">Clear</button>

                                <!-- SORT -->
                                <button @click="sort('followerscount')" type="button" class="btn btn-outline-light btn-sm">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-sort-up" viewBox="0 0 16 16">
                                        <path d="M3.5 12.5a.5.5 0 0 1-1 0V3.707L1.354 4.854a.5.5 0 1 1-.708-.708l2-1.999.007-.007a.498.498 0 0 1 .7.006l2 2a.5.5 0 1 1-.707.708L3.5 3.707V12.5zm3.5-9a.5.5 0 0 1 .5-.5h7a.5.5 0 0 1 0 1h-7a.5.5 0 0 1-.5-.5zM7.5 6a.5.5 0 0 0 0 1h5a.5.5 0 0 0 0-1h-5zm0 3a.5.5 0 0 0 0 1h3a.5.5 0 0 0 0-1h-3zm0 3a.5.5 0 0 0 0 1h1a.5.5 0 0 0 0-1h-1z" />
                                    </svg>
                                    <span class="visually-hidden"> Fllwrs</span>
                                </button>
                                <button @click="sort('timestampms')" type="button" class="btn btn-outline-light btn-sm">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-sort-up" viewBox="0 0 16 16">
                                        <path d="M3.5 12.5a.5.5 0 0 1-1 0V3.707L1.354 4.854a.5.5 0 1 1-.708-.708l2-1.999.007-.007a.498.498 0 0 1 .7.006l2 2a.5.5 0 1 1-.707.708L3.5 3.707V12.5zm3.5-9a.5.5 0 0 1 .5-.5h7a.5.5 0 0 1 0 1h-7a.5.5 0 0 1-.5-.5zM7.5 6a.5.5 0 0 0 0 1h5a.5.5 0 0 0 0-1h-5zm0 3a.5.5 0 0 0 0 1h3a.5.5 0 0 0 0-1h-3zm0 3a.5.5 0 0 0 0 1h1a.5.5 0 0 0 0-1h-1z" />
                                    </svg>
                                    <span class="visually-hidden"> Nwst</span>
                                </button>

                                <!-- INFO -->
                                <button type="button" class="tweet-stream-info btn btn-outline-dark align-middle inline ml-2" style="border: none;" data-toggle="modal" data-target="#tweetStreamInfoModal">
                                    <span class="visuallyhidden">Tweetstream info</span>
                                    <img style="width: 20px;" src="@/assets/img/icons/ui/question.svg" alt="" />
                                </button>

                                <!-- FILTER TWEETS -->
                                <div class="input-group input-group-sm mb-3">
                                    <div class="input-group-prepend">
                                        <span class="input-group-text" id="inputGroup-sizing-sm">Search tweets</span>
                                    </div>
                                    <input type="text" class="form-control" id="filterTweets" value="" aria-label="Search tweet stream" aria-describedby="Search tweet stream">
                                </div>
                                <h2 class='tweet-stream-info-in-stream hidden'>Tweet stream is paused.</h2>
                            </div>
                        </div>
                    </nav>
                    <div class="col-md-12 m-0 p-0 mr-2 mt-1">
                        <div style="font-family: courier; font-weight: bold;font-size: 1.3em; color: #eee;" class="console"><span class="timestamp">-</span>: <span class="message">-</span></div>
                        <!-- <h2 class="header-tweets-realtime " style="display: inline;">Realtime</h2> -->
                    </div>
                    <div class="row m-0 p-0">
                        <div class=" col-md-12 m-0 p-0">
                            <div class="tweets row m-0 p-0"></div>
                        </div>
                    </div>
                </div>

                <!-- SELECTED TWEETS -->
                <div class="tweets-selected col-md-12 m-0 p-0" style="overflow: scroll;">
                    <nav class="navbar navbar-expand-md sticky-top pt-0 pb-0 pl-2 pr-2 " style="background: #005B81;">
                        <div class="row m-0 p-0" style="width: 100%;">
                            <div class="col-xs-6 m-0 p-0 mr-2">
                                <h2 class="ml-1 mt-2 header-tweets-selected">Bookmarked <button style="transform: translateY(-0.2em);" class="m-0 tweets-selected-open-close-button"><span class="visuallyhidden">open / close selected tweets panel</span></button></h2>
                            </div>

                            <div class="col-xs-6 m-0 p-0 mt-1 ">
                                <button class="btn btn-sm btn-outline-light float-right inline clear-selected-tweets-button">Clear</button>
                                <button class="copyBookmarkedURLsToClipboard btn btn-sm btn-outline-light" style="" title="Copy Links">Copy All</button>
                                <button class="copyBookmarkedURLsToEmail btn btn-sm btn-outline-light" style="" title="Copy to email">Email</button>
                            </div>
                        </div>
                    </nav>

                    <div class="row m-0 ml-2 mr-2 p-0">
                        <div class="col-md-12 m-0 p-0">
                            <div class="tweets row m-0 p-0"></div>
                        </div>
                    </div>
                </div>
            </div>
            <!-- END own content -->
        </div>

        <input type="checkbox" id="open-button" />
        <label class="menu-icon" for="open-button">
            <div class="arrow-tweet-panel-wrap rotate180">
                <svg class="arrow-tweet-panel" width="43" height="18" viewBox="0 0 43 18">
                    <path d="M41.895 6.484C38.58 4.165 35.151 1.338 31.265.077c-1.677-.544-3.236 1.906-1.79 3.075a134.635 134.635 0 003.892 3.022c-3.56-.113-7.222.252-10.626.217-7.208-.076-14.428-.378-21.633-.02-1.479.072-1.478 2.216 0 2.296 11.347.615 22.721.397 34.056.903-1.218.691-2.47 1.328-3.692 2.027-2.079 1.19-3.956 2.381-4.225 4.921-.067.633.602 1.211 1.195 1.195 2.54-.064 4.678-1.886 6.861-3.013 2.528-1.303 4.939-2.609 7.07-4.514 1.214-1.085.692-2.885-.477-3.702" fill-rule="evenodd" /></svg>
            </div>
            <span></span>
            <span class="visuallyhidden">Open/Close Menu</span>
        </label>
    </div>
</div>
</template>

<script>
import TwitterRealTimeStartStopToggle from "@/components/TwitterRealTimeStartStopToggle.vue";

import {
    getJSON
} from "@/assets/js/getJSON.js";
import {
    realTimeTweets
} from "@/assets/js/realTimeTweets.js";
import {
    disableBodyScrollMixin
} from "./mixins/disableBodyScroll";

import {
    recalculateTweetTimeStamps
} from "@/assets/js/calculateTweetTimeStamps"

import {
    sort
} from "@/assets/js/sortTweets.js";

import Typewriter from "@/components/AnimatedCharacters/Typewriter.vue";

export default {
    name: "twitterRealtime",
    data() {
        return {};
    },
    mixins: [disableBodyScrollMixin],
    components: {
        TwitterRealTimeStartStopToggle,
        Typewriter
    },
    mounted() {
        setTimeout(function () {
            getJSON.start()
        }, 10000);
        this.hideThisTweet();
        this.copyTweet();
        // this.startStopTweetStream();
        this.disableBodyScroll(".content"); //mixin
        // this.disableBodyScroll(".tweets-realtime"); //mixin
        // this.disableBodyScroll(".tweets-selected"); //mixin
        this.drawAttentionToTwitter();
        this.removeNewTweetsSign();
        // this.showAllTweets();
        this.toggleSelectedTweetsPanel();
        this.clearTweetStream();
        this.clearSelectedTweets();
        this.filterTweets();
        this.getBookmarkedTweetsFromLocalStorage();
        this.getRealtimeTweetsFromLocalStorage();
        this.setRealtimeTweetsToLocalStorageBeforeUnload();
        this.clock();
        this.insertAndRemoveMessageToTweetStream();
        recalculateTweetTimeStamps();
        this.sortKeybindings();
    },
    methods: {
        sort(key) {
            sort(key);
        },
        sortKeybindings() {
            Mousetrap.bind(['t f'], function () {
                sort('followerscount');
                return false;
            });

            Mousetrap.bind(['t n'], function () {
                sort('timestampms');
                return false;
            });
        },
        hideThisTweet() {
            document.addEventListener("click", function (event) {
                // tweets
                if (event.target.matches(".tweets-container .tweet .card-body button.close")) {
                    var selectedTweet = event.target.closest(".tweet");
                    selectedTweet.style.display = 'none';
                }
                // messages in between tweets
                if (event.target.matches(".tweets-container .tweet-stream-messages button.close")) {
                    var selectedTweet = event.target.closest(".tweet-stream-messages");
                    selectedTweet.style.display = 'none';
                }
            }, false);
        },
        clock() {
            // https://codepen.io/afarrar/pen/JRaEjP
            function showTime() {
                var clock = document.querySelector('.console .timestamp');

                var date = new Date();
                var h = date.getHours(); // 0 - 23
                var m = date.getMinutes(); // 0 - 59
                var s = date.getSeconds(); // 0 - 59
                // var session = "AM";

                // if (h == 0) {
                //     h = 12;
                // }

                // if (h > 12) {
                //     h = h - 12;
                //     session = "PM";
                // }

                h = (h < 10) ? "0" + h : h;
                m = (m < 10) ? "0" + m : m;
                s = (s < 10) ? "0" + s : s;

                // var time = h + ":" + m + ":" + s + " " + session;
                var time = h + ":" + m + ":" + s;
                clock.innerText = time;
                clock.textContent = time;

                setTimeout(showTime, 1000);
            }
            showTime();

        },
        getBookmarkedTweetsFromLocalStorage() {
            var selectedTweets = document.querySelector('.tweets-selected .tweets');
            var val;
            if (localStorage.getItem("bookmarkedTweets") !== null) {
                val = localStorage.getItem("bookmarkedTweets");
                selectedTweets.insertAdjacentHTML("afterbegin", val);
            }
        },
        setBookmarkedTweetsToLocalStorage() {
            var selectedTweets = document.querySelector('.tweets-selected .tweets');
            localStorage.setItem("bookmarkedTweets", selectedTweets.innerHTML);
        },
        getRealtimeTweetsFromLocalStorage() {
            var realtimeTweets = document.querySelector('.tweets-realtime .tweets');
            var val;
            if (localStorage.getItem("realtimeTweets") !== null) {
                val = localStorage.getItem("realtimeTweets");
                realtimeTweets.insertAdjacentHTML("afterbegin", val);
            }
        },
        setRealtimeTweetsToLocalStorage() {
            var realtimeTweets = document.querySelector('.tweets-realtime .tweets');
            localStorage.setItem("realtimeTweets", realtimeTweets.innerHTML);
        },
        setRealtimeTweetsToLocalStorageBeforeUnload() {
            var that = this;

            // new tweets are deliverd every 10 sec, hence 10000
            setInterval(function () {
                that.setRealtimeTweetsToLocalStorage();
            }, 10000);

            // doesn't seem to work
            // document.addEventListener('beforeunload', function () {
            //     that.setRealtimeTweetsToLocalStorage();
            // }, false);
        },
        filterTweets() {
            // https://schier.co/blog/2014/12/08/wait-for-user-to-stop-typing-using-javascript.html
            var domTextInput = document.querySelector("#filterTweets");
            var domBody = document.querySelector("body");
            var tweets = document.querySelectorAll(".tweet");
            // Init a timeout variable to be used below
            var timeout = null;

            // THROTTLING
            // https://remysharp.com/2010/07/21/throttling-function-calls
            function throttle(fn, threshhold, scope) {
                threshhold || (threshhold = 250);
                var last,
                    deferTimer;
                return function () {
                    var context = scope || this;

                    var now = +new Date,
                        args = arguments;
                    if (last && now < last + threshhold) {
                        // hold on to it
                        clearTimeout(deferTimer);
                        deferTimer = setTimeout(function () {
                            last = now;
                            fn.apply(context, args);
                        }, threshhold);
                    } else {
                        last = now;
                        fn.apply(context, args);
                    }
                };
            }

            function showResults(searchString) {
                showAllEntries();

                if (searchString !== "") { // als er iets in het zoekveld staat
                    tweets = document.querySelectorAll(".tweet");
                    for (var i = 0; i < tweets.length; i++) {
                        // first hide all
                        tweets[i].classList.add("hideSearchResult");

                        // if searchstring is found then remove class that hides result
                        if (
                            tweets[i].innerHTML.toLowerCase().indexOf(searchString.toLowerCase()) > -1
                        ) {
                            tweets[i].classList.remove("hideSearchResult");
                        }
                    }
                } else { // when nothing in search field (anymore) all tweets should be shown again
                    showAllEntries();
                    domBody.classList.remove("condensedLayout");
                }
            }

            function showAllEntries() {
                for (var i = 0; i < tweets.length; i++) {
                    tweets[i].classList.remove("hideSearchResult");
                }
            }

            function undoSearchResults() {
                showAllEntries();
            }

            domTextInput.addEventListener("click", function () {
                undoSearchResults();
                this.value = "";
            }, false);

            // Listen for keystroke events
            domTextInput.addEventListener("keyup", throttle(function () {
                showResults(domTextInput.value);
            }, 1000), false);
        },
        clearTweetStream() {
            var that = this;
            var button = document.querySelector('.clear-tweet-stream-button');
            var tweets = document.querySelector('.tweets-realtime .tweets');

            function clear() {
                tweets.innerHTML = "";
                that.setRealtimeTweetsToLocalStorage();
            }

            button.addEventListener('click', function () {
                clear();
            }, false);

            Mousetrap.bind(['t c'], function () {
                clear();
                return false;
            });
        },
        clearSelectedTweets() {
            var that = this;
            var button = document.querySelector('.clear-selected-tweets-button');
            var tweets = document.querySelector('.tweets-selected .tweets');
            button.addEventListener('click', function () {
                tweets.innerHTML = "";
                that.setBookmarkedTweetsToLocalStorage();
            }, false);
        },
        toggleSelectedTweetsPanel() {
            var panel = document.querySelector('.tweets-selected');
            var trigger = document.querySelector('.tweets-selected-open-close-button');

            trigger.addEventListener('click', function () {
                panel.classList.toggle('open');
            }, false);

        },
        showAllTweets() {
            document.querySelector('#showAllTweets').addEventListener('change', function () {
                var tweetStreamConfiguration = document.querySelector('.tweet-stream-configuration');
                realTimeTweets.toggleAllTweets();
                tweetStreamConfiguration.disabled = !tweetStreamConfiguration.disabled;
            }, false);
        },
        removeNewTweetsSign() {
            document.querySelector(".menu-icon").addEventListener('click', function () {
                this.classList.remove('new-tweets');
            }, false);
        },
        drawAttentionToTwitter() {
            var button = document.querySelector(".menu-icon");
            var effectInterval = 0 // to be used for clearing setInterval
            var interval = 3000;
            var animationLength = 2000; // waiting time before class is removed after adding (to start animation)
            function startEffect() {
                var type = "highlighter";
                button.classList.add(type);
                setTimeout(function () {
                    document.querySelector(".menu-icon").classList.remove(type);
                }, animationLength);
                interval += 9000; // simple way to increase intervals to avoid annoyed users
                clearInterval(effectInterval);
                effectInterval = setInterval(startEffect, interval);
            }

            effectInterval = setInterval(startEffect, interval);

            // stop the effect after the first time the realtime tweets button is clicked
            button.addEventListener("click", function () {
                clearInterval(effectInterval);
            }, false);
        },
        copyTweet() {
            var that = this;
            document.addEventListener("click", function (event) {
                if (event.target.matches(".tweets-container .tweet .card-body button.select-tweet")) {
                    var selectedTweet = event.target.closest(".tweet");
                    // document.querySelector(".tweets-selected .tweets").innerHTML = "";
                    document.querySelector(".tweets-selected .tweets").insertAdjacentElement('afterbegin', selectedTweet);

                    that.setBookmarkedTweetsToLocalStorage();
                }
            }, false);
        },
        insertAndRemoveMessageToTweetStream() {
            var container = document.querySelector(".tweets-realtime .tweets");

            // array that will contain all keys in language.tweetStream
            var allTweetStreamMessages = [];

            function insertAndRemoveMessage(a) {
                var string = "<button class='close'><span class='visuallyhidden'>remove this tweet</span>×</button>";
                var div = document.createElement("div");
                div.classList.add('tweet-stream-messages');
                div.classList.add('card');
                div.insertAdjacentHTML("afterbegin", string);
                div.insertAdjacentHTML("beforeend", a);

                // add
                container.insertAdjacentElement("afterbegin", div);

                // remove
                setTimeout(function () {
                    container.removeChild(div);
                }, 12000);
            }

            //How to randomize (shuffle) a JavaScript array?
            //https://stackoverflow.com/a/2450976
            function shuffle(array) {
                var currentIndex = array.length,
                    temporaryValue, randomIndex;

                // While there remain elements to shuffle...
                while (0 !== currentIndex) {

                    // Pick a remaining element...
                    randomIndex = Math.floor(Math.random() * currentIndex);
                    currentIndex -= 1;

                    // And swap it with the current element.
                    temporaryValue = array[currentIndex];
                    array[currentIndex] = array[randomIndex];
                    array[randomIndex] = temporaryValue;
                }

                return array;
            }

            // push all keys in language.tweetStream into array that we can shuffle
            for (var k in language.tweetStream) {
                if (language.tweetStream.hasOwnProperty(k)) {
                    allTweetStreamMessages.push(k);
                }
            }

            shuffle(allTweetStreamMessages);

            // insert a message from the shuffled array. Array will be re-shuffled
            (function () {
                var i = 0;
                setInterval(function () {
                    if (i >= allTweetStreamMessages.length) {
                        i = 0;
                        shuffle(allTweetStreamMessages);
                    }
                    // allTweetStreamMessages as key for language.tweetStream
                    insertAndRemoveMessage(language.tweetStream[allTweetStreamMessages[i]]);
                    i++;
                }, 500000);
            }())

            setTimeout(function () {
                insertAndRemoveMessage(language.tweetStream.message1);
            }, 60000);

            setTimeout(function () {
                insertAndRemoveMessage(language.tweetStream.message5);
            }, 100000);

            setTimeout(function () {
                insertAndRemoveMessage(language.tweetStream.message6);
            }, 180000);

            // setTimeout(function () {
            //     insertAndRemoveMessage(language.tweetStream.message1);
            // }, 100000);

            setTimeout(function () {
                insertAndRemoveMessage(language.tweetStream.message1);
            }, 250000);

            setTimeout(function () {
                insertAndRemoveMessage(language.tweetStream.message1);
            }, 360000);
        }
    }
};

// TIP: open menu initially by adding this class to body: show-menu, and set isOpen = true;
function slideInMenu() {
    "use strict";
    var bodyEl = document.body,
        openbtn = document.getElementById("open-button"),
        openbtn2 = document.querySelector(".twitter-open-close-handle"),
        isOpen = false; // see above

    function init() {
        initEvents();
    }

    function initEvents() {
        const mediaQuery = window.matchMedia('(min-width: 768px)');
        if (openbtn) openbtn.addEventListener("click", toggleMenu);
        if (openbtn2) openbtn2.addEventListener("click", toggleMenu);

        Mousetrap.bind(['o'], function () {
            toggleMenu()
            return false;
        });

        // Create a media condition that targets viewports at least 768px wide
        // Medium devices (tablets, 768px and up) The navbar toggle appears at this breakpoint
        // Toggle menu to show tweet stream initially only on bigger screens
        if (mediaQuery.matches) {
            // open the tweetstream only once
            if (localStorage.getItem("tweetStreamOpenedOnce") !== "true") {
                toggleMenu();
                setTimeout(function () {
                    toggleMenu();
                }, 700);

                localStorage.setItem("tweetStreamOpenedOnce", "true");
            }
        }

        if (isOpen === true && document.querySelector("#open-button")) {
            document.querySelector("#open-button").setAttribute("checked", "checked");
        }
    }

    function toggleMenu() {
        var arrowTweetPanelWrap = document.querySelector(".arrow-tweet-panel-wrap");
        if (isOpen) {
            bodyEl.classList.remove("show-menu");
            if (arrowTweetPanelWrap) {
                arrowTweetPanelWrap.classList.add("rotate180");
            }
        } else {
            bodyEl.classList.add("show-menu");
            if (arrowTweetPanelWrap) {
                arrowTweetPanelWrap.classList.remove("rotate180");
            }
        }
        isOpen = !isOpen;
    }

    // setTimeout(toggleMenu, 500);

    init();
}

document.addEventListener("DOMContentLoaded", function () {
    slideInMenu();
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style lang="scss" scoped>
/***********************/
/* BEGIN CONFIGURATION */
/***********************/

// for instructions on how to have menu opened onload see comment in slideInMenu.vue JS part

$zIndex: 1021; // bootstrap sticky menu is 1020
$hamburgerPadding: 6px;
$hamburgerWidth: 40px;
$hamburgerHeight: 40px;
$hamburgerLinesHeight: 3px;
$hamburgerPositionTop: 10px;
$hamburgerPositionLeft: 10px;
$hamburgerLinesColor: #2A3166;
$hamburgerBackgroundColor: #cae7df60;
// $hamburgerBoxShadow: 0px 0px 37px 0px rgba(0, 0, 0, 0.75);
// $hamburgerBoxShadow: 0px 0px 1px 0px #000000;
$hamburgerBoxShadow: none;

// how wide should the menu be. 100% covers whole screen
$menuWidth: 300px;
// $menuWidth: 100%;

*,
*:before,
*:after {
    box-sizing: border-box;
}

#slide-menu-and-buttons-wrapper {
    color: #222;

}

.slide-menu-wrapper {
    background: #1da1f2;

    // width of the menu:

}

h2 {
    text-transform: none;
}

.content {
    padding: 1.5em 0.5em 2em;
    text-align: left;
    max-width: 40em;
    margin: 0 auto;
    // border: 5px solid red;
    // makes slide in menu vertical scrollable:
}

ul {
    // font-size: 0.9em;
    margin: 0;
    padding: 0;
}

li {
    border: 3px solid rgba(231, 57, 57, 0.329);
    display: inline-block;
    margin: 0.2em;
}

li a {
    padding: 0.5em;
    color: #333;
}

// li a:visited {
//     border: 3px solid green !important;
//     // color: red;
// }

/*********************/
/* Added styles */
/*********************/

/*********************/
/* END CONFIGURATION */
/*********************/

/* 
BASED ON: CODROPS
https://tympanus.net/codrops/2014/09/16/off-canvas-menu-effects/ 
*/

#slide-menu-and-buttons-wrapper {
    position: fixed;
    top: 0;
    right: 0;
    margin: 0;
    padding: 0;
    z-index: $zIndex;
}

.slide-menu-wrapper {
    position: fixed;
    top: 0;
    right: 0;
    height: 100%;
    width: 100%;
    max-width: 500px;
    margin: 0 !important;
    padding: 0 !important;
    transform: translate3d(100%, 0, 0);
    transition: transform 0.4s;
    box-shadow: 0px 0px 37px 0px rgba(0, 0, 0, 0.75);
}

.content {
    height: 100%;
    overflow: scroll;
    font-size: 0.8em;
}

// .menu-button {
//     position: fixed;
//     top: 10px;
//     left: 5px;
//     z-index: $zIndex;
// }

.menu-button:hover {
    opacity: 0.6;
}

/* Shown menu */
.show-menu .slide-menu-wrapper {
    transform: translate3d(0, 0, 0);
    transition: transform 0.4s;
    transition-timing-function: cubic-bezier(0.7, 0, 0.3, 1);
}

.show-menu .content::before {
    opacity: 1;
    transition: opacity 0.4s;
    transition-timing-function: cubic-bezier(0.7, 0, 0.3, 1);
    transform: translate3d(0, 0, 0);
}

/* HAMBURGER */
// https://codepen.io/perjor/pen/yOzZPj
#open-button {
    display: none;
}

.menu-icon {
    background: url(../assets/img/twitter/Twitter_Logo_Blue.svg);
    box-shadow: $hamburgerBoxShadow;
    // position of twitter icon when tweet panel is closed
    position: fixed;
    top: 5px;
    left: -140px;
    display: block;
    cursor: pointer;
    height: $hamburgerHeight;
    width: $hamburgerWidth;
    padding: $hamburgerPadding;
    z-index: $zIndex;
    border-radius: 50%;
}

.menu-icon.new-tweets:after {
    content: ".";
    position: absolute;
    top: 5px;
    right: 0;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: red;
}

.menu-icon:before {
    content: "";
    position: absolute;
    top: 3px;
    left: 0;
    border-radius: 50%;
}

.menu-icon.disconnected:before {
    background: url(../assets/img/icons/ui/no-entry.svg) no-repeat;
    background-size: contain;
    width: 12px;
    height: 12px;
}

// position of twitter icon when tweet panel is opened
.show-menu .menu-icon {
    background: url(../assets/img/twitter/Twitter_Logo_WhiteOnBlue.svg);
    left: auto;
    right: 2em;
}

.tweets-realtime {
    padding-bottom: 150%;
}

.tweets-selected {
    position: fixed;
    bottom: 0;
    left: 0;
    background: #005B81;
    box-shadow: 0px 0px 37px 0px rgba(0, 0, 0, 0.75);
    height: 95%;
    transform: translate3d(0, 85%, 0);
    transition: transform 0.4s;
    transition-timing-function: cubic-bezier(0.7, 0, 0.3, 1);
    z-index: 1021; // one higher than the bootstrap nav
}

.tweets-selected.open {
    transform: translate3d(0, 0, 0);
    transition: transform 0.4s;
    transition-timing-function: cubic-bezier(0.7, 0, 0.3, 1);

}

.tweets-selected-open-close-button {
    background: url("../assets/img/icons/jv-creative/tweets-selected-open.png") no-repeat center;
    background-size: 20px;
    width: 30px;
    height: 30px;
}

.open .tweets-selected-open-close-button {
    background: url("../assets/img/icons/jv-creative/tweets-selected-close.png") no-repeat center;
    background-size: 20px;
    width: 30px;
    height: 30px;
}

.header-tweets-realtime,
.header-tweets-selected {
    color: #eee;
    font-family: poppinsbold;
    font-size: 1.3em;
}

.select-tweet {
    background: linear-gradient(to right, #5C34A7, #2376D6);

}

// .tweets-selected .select-tweet,
.tweets-selected img,
.tweets-selected .extra-info {
    display: none;
}

// https://codepen.io/etreacy/pen/ZJYoRV
.highlighter {
    animation-name: highlighter;
    animation-duration: 3s;
    animation-fill-mode: forwards;
    // animation-timing-function: cubic-bezier(0.1, 0.7, 1.0, 0.1);
    animation-timing-function: ease-in-out;
}

.twitter-open-close-handle {
    position: absolute;
    top: 50%;
    transform: translateY(calc(-76px*0.8));
    left: calc(-36px*0.8);
    background: url(../assets/img/icons/jv-creative/twitter-open-close-handle.svg) no-repeat;
    background-size: contain;
    width: calc(36px*0.8);
    height: calc(76px*0.8);
    cursor: pointer;
    display: none;
}

/* Medium devices (tablets, 768px and up) The navbar toggle appears at this breakpoint */
@media (min-width: 768px) {
    .twitter-open-close-handle {
        display: block;
    }
}

#filterTweets {
    font-size: 18px;
}

@keyframes highlighter {
    0% {
        background-color: transparent;
    }

    10% {
        background-color: #be4a06;
    }

    100% {
        background-color: transparent;
    }
}

// END HAMBURGER

//ARROW IN TWEET PANEL OPENER
//https://codepen.io/Nonoroazoro/pen/xWdPNp

// initial, .rotate180 makes arrow point to left
.arrow-tweet-panel-wrap.rotate180,
.arrow-tweet-panel {
    // 43 : 18, see inline <svg>
    width: 40px;
    height: 17px;
}

// when tweet panel open, class rotate180 removed
.arrow-tweet-panel-wrap,
.arrow-tweet-panel {
    // 43 : 18, see inline <svg>
    width: 25px;
    height: 10px;
}

.arrow-tweet-panel-wrap.rotate180 {
    margin-left: -15px !important;
    margin-top: 25px;
}

.arrow-tweet-panel-wrap {
    margin-left: 0px;
    margin-top: 19px;

}

.arrow-tweet-panel-wrap .arrow-tweet-panel path {
    fill: #eee
}

.arrow-tweet-panel-wrap.rotate180 .arrow-tweet-panel path {
    fill: #1CA1F2;
    // fill: #EEE;
}

.arrow-tweet-panel-wrap .arrow-tweet-panel {
    animation: arrow-tweet-panel-pulse 0.82s ease-in-out infinite;
}

.rotate90 {
    transform: rotate(90deg);
}

.rotate180 {
    transform: rotate(180deg);
}

.rotate270 {
    transform: rotate(270deg);
}

@keyframes arrow-tweet-panel-pulse {

    0%,
    to {
        transform: translateZ(0);
    }

    50% {
        transform: translate3d(1px, 0, 0);
    }
}

//END ARROW IN TWEET PANEL OPENER
</style>
