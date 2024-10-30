<script setup>
    import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome';
    import { faFacebook, faLinkedin, faXTwitter, faInstagram, faDribbble  } from '@fortawesome/free-brands-svg-icons';

    const props = defineProps({
        imageSrc: String,
        fbLink: String,
        lILink: String,
        xLink: String,
        instaLink: String,
        dribLink: String,
        followLink: String,
        messageLink: String
    });

    console.log(props.imageSrc);
</script>

<template>
    <article>
        <div id="image-container">
            <img :src="imageSrc">
        </div>
        <div id="svg-container">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320">
                <path fill="#ffffff" fill-opacity="1" d="M0,224L60,202.7C120,181,240,139,360,149.3C480,160,600,224,720,234.7C840,245,960,203,1080,186.7C1200,171,1320,181,1380,186.7L1440,192L1440,320L1380,320C1320,320,1200,320,1080,320C960,320,840,320,720,320C600,320,480,320,360,320C240,320,120,320,60,320L0,320Z"></path>
            </svg>
        </div>
        <div id="content">
            <div id="hero">
                <h3>
                    <slot name="name">NAME SURNAME</slot>
                </h3>
                <p>
                    <slot name="handle">@namesurname</slot>
                </p>
            </div>
            <div id="socials">
                <a :href="fbLink" target="_blank"><FontAwesomeIcon :icon="faFacebook"></FontAwesomeIcon></a>
                <a :href="lILink" target="_blank"><FontAwesomeIcon :icon="faLinkedin"></FontAwesomeIcon></a>
                <a :href="xLink" target="_blank"><FontAwesomeIcon :icon="faXTwitter"></FontAwesomeIcon></a>
                <a :href="instaLink" target="_blank"><FontAwesomeIcon :icon="faInstagram"></FontAwesomeIcon></a>
                <a :href="dribLink" target="_blank"><FontAwesomeIcon :icon="faDribbble"></FontAwesomeIcon></a> 
            </div>
            <div id="about">
                <slot name="about-copy">
                    A little paragraph about the profile. Lorem ipsum blah blah blah. iewhfiwhefihw Lorem ipsum blah blah blah. iewhfiwhefihw Lorem 
                </slot>
            </div>
        </div>
        <div id="ctas">
            <a :href="followLink" target="_blank"><button>Follow</button></a>
            <a :href="messageLink" target="_blank"><button>Message</button></a>
        </div>
    </article>
</template>

<style scoped>

    article{
        height: 480px;
        width: 320px;
        background-color: #FFFFFF;
        border-radius: 40px;
        text-align: center;
        color: #060606;
        box-shadow: 0px 0px 15px #D7DBC0;
        position: relative;
    }

    h3{
        font-size: 1.5rem;
        margin-bottom: 0;
    }

    #image-container{
        height: calc(480px / 3);
        background-color: #993250;
        border-radius: inherit;
    }

    img{
        height: 100px;
        width: 100px;
        border-radius: 100%;
        margin-top: 4%;
        object-fit: cover;
    }

    #svg-container{
        position: absolute;
        top: 89px;
        width: 100%;
        height: fit-content;
    }

    #hero > p
    {
        margin: 0;
        color: #A2A2A2;
    }

    #socials > a > svg{
        margin: 25px 12px 25px 12px;
        font-size: 1.2rem;
        color:#060606;
    }

    #about{
        padding: 0 28px 0 28px;
    }

    #ctas{
        position: absolute;
        bottom: 20px;
        width: 100%;
        display: flex;
        flex-direction: row;
        justify-content: center;
        gap: 30px;
    }

    button{
        text-decoration: none;
        width: 120px;
        height: 35px;
        color: #A2A2A2;
        border-radius: 300px;
    }

    button:hover{
        cursor: pointer;
    }

    a:nth-child(1) > button
    {
        background-color: #E0408A;
        border: 0;
        color: #FFFFFF;
    }
    
    a:nth-child(2) > button
    {
        background-color: #FFFFFF;
        border: 1px solid;
        color: #E0408A;
    }
</style>
