---
layout: page
title: About Me
permalink: /about_me/
---
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/devicon.min.css">

1. 
{:toc}

My name is Zane Clark and I go by the username Ketexon.

I am a <span id="age"></span> year old student who finds joy in academia and creativity.

# Hobbies

## Programming

I have been programming for about 6 years, and it is one of the hobbies in which I spend most of my time. I hope to major in computer science at University.

### Languages
In order of subjective skill level:

<div class="container language-container h1"></div>

I have also worked with x86 assembly (NASM), Lua, SQL, MongoDB, HTML5, and CSS3/SASS.

### Frameworks, Libraries, APIs

<div class="container frameworks-container h1"></div>

I have also worked with [OpenGL]{:target="_blank"}, [Vulkan]{:target="_blank"}, [SDL2]{:target="_blank"}, [Amethyst]{:target="_blank"}, [Love2D]{:target="_blank"}

### Engines, IDEs, Text Editors, and Environments

<div class="container ide-container h1"></div>

I also use Notepad++, Android Studio, and Unity.


### Build tools, Compilers, and Package Managers

<div class="container build-container h1"></div>

I also use Make, Cargo, MSVC, MinGW, pip, and GNU GCC.

[OpenGL]:https://www.opengl.org/
[Vulkan]:https://www.khronos.org/vulkan/
[SDL2]:https://www.libsdl.org/
[Amethyst]:https://amethyst.rs/
[Love2D]:https://love2d.org/
<script>
const languages = [
	{
		ico: "cplusplus",
		name: "C++",
		skill: "advanced",
		when: "2018-now"
	},
	{
		ico: "python",
		name: "Python",
		skill: "advanced",
		when: "2018-now"
	},
	{
		ico: "javascript",
		name: "Javascript",
		skill: "advanced",
		when: "2014-now"
	},
	{
		ico: "java",
		name: "Java",
		skill: "intermediate",
		when: "2015-2018"
	},
	{
		ico: "php",
		name: "Java",
		skill: "intermediate",
		when: "2015-2016"
	},
	{
		ico: "rust",
		name: "Rust",
		skill: "low intermediate",
		when: "2021-now"
	},
	{
		ico: "c",
		name: "C",
		skill: "high beginner"
	},
	{
		ico: "csharp",
		name: "C#",
		skill: "high beginner"
	},
	{
		ico: "fsharp",
		name: "F#",
		skill: "beginner",
		when: "2021"
	},
	{
		ico: "scala",
		name: "Scala",
		skill: "beginner",
		when: "2020"
	},
];
const defaultIconSuffix = "plain"
let languageContainer = document.querySelector(".language-container");
for(let langInfo of languages){
	let icon = document.createElement("i");
	icon.classList.add(`devicon-${langInfo.ico}-${langInfo.suffix || defaultIconSuffix}`);
	icon.classList.add("tooltip-hover");
	icon.dataset.bsToggle = "tooltip";
	icon.dataset.bsPlacement = "bottom";
	icon.title = `${langInfo.name}, ${langInfo.skill}${langInfo.when ? ", "+ langInfo.when : ""}`;
	languageContainer.appendChild(icon);
}

const frameworks = [
	{
		ico: "bootstrap",
		name: "Bootstrap",
		skill: "beginner",
		when: "2021-now"
	},
	{
		ico: "express",
		name: "Express JS",
		skill: "beginner",
		when: "2019",
		suffix: "original"
	},
	{
		ico: "materialui",
		name: "Material UI",
		skill: "intermediate",
		when: "2019-now"
	},
	{
		ico: "react",
		name: "React JS",
		skill: "intermediate",
		when: "2019-now"
	},
];
let frameworksContainer = document.querySelector(".frameworks-container");
for(let fwInfo of frameworks){
	let icon = document.createElement("i");
	icon.classList.add(`devicon-${fwInfo.ico}-${fwInfo.suffix || defaultIconSuffix}`);
	icon.classList.add("tooltip-hover");
	icon.dataset.bsToggle = "tooltip";
	icon.dataset.bsPlacement = "bottom";
	icon.title = `${fwInfo.name}, ${fwInfo.skill}${fwInfo.when ? ", "+ fwInfo.when : ""}`;
	frameworksContainer.appendChild(icon);
}


const ides = [
	{
		ico: "visualstudio",
		name: "Visual Studio/Visual Studio Code"
	},
	{
		ico: "vim",
		name: "Vim"
	},
	{
		ico: "intellij",
		name: "IntelliJ IDEA"
	}
];
let ideContainer = document.querySelector(".ide-container");
for(let ideInfo of ides){
	let icon = document.createElement("i");
	icon.classList.add(`devicon-${ideInfo.ico}-${ideInfo.suffix || defaultIconSuffix}`);
	icon.classList.add("tooltip-hover");
	icon.dataset.bsToggle = "tooltip";
	icon.dataset.bsPlacement = "bottom";
	icon.title = `${ideInfo.name}`;
	ideContainer.appendChild(icon);
}

const buildTools = [
	{
		ico: "babel",
		name: "Babel",
	},
	{
		ico: "npm",
		name: "NPM",
	},
	{
		ico: "webpack",
		name: "Webpack",
	},
];
let buildToolsContainer = document.querySelector(".build-container");
for(let btInfo of buildTools){
	let icon = document.createElement("i");
	icon.classList.add(`devicon-${btInfo.ico}-${btInfo.suffix || defaultIconSuffix}`);
	icon.classList.add("tooltip-hover");
	icon.dataset.bsToggle = "tooltip";
	icon.dataset.bsPlacement = "bottom";
	icon.title = `${btInfo.name}`;
	buildToolsContainer.appendChild(icon);
}

document.querySelector("#age").appendChild(
	document.createTextNode(
		Math.floor((Date.now() - new Date("01 August 2003").getTime())/1000/60/60/24/365)
	)
)
</script>