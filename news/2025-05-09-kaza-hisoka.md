---
title: "انت هو انت"
date: 2025-05-09
image: https://media1.thehungryjpeg.com/thumbs/800_3841851_qx3933imzjf7rur4h8ed46s2llddsu0shv68uncs.jpg
category: مأسات
badge: غريب
---
كن يقضا دوما يا خبيبي
let fileContent = readFile("salah/salah.txt");
let regex = /<dt>(.*?)<\/dt>\s*<dd[^>]*>\s*<span>\s*(\d{1,2}:\d{2})\s*<\/span>\s*([AP]M)/g;
let matches = fileContent.match(regex);
let prayerTimes = [];

for (let i = 0; i < matches.length; i++) {
  let match = matches[i].match(/<dt>(.*?)<\/dt>\s*<dd[^>]*>\s*<span>\s*(\d{1,2}:\d{2})\s*<\/span>\s*([AP]M)/);
  let time = match[2].split(":");
  let hours = parseInt(time[0]);
  let minutes = time[1];
  
  if (match[3] === "PM" && hours !== 12) {
    hours += 12;
  } else if (match[3] === "AM" && hours === 12) {
    hours = 0;
  }
  
  prayerTimes.push(`${hours.toString().padStart(2, '0')}:${minutes}`);
}

let salah = prayerTimes.join("\n");
writeFile("salah/salah.txt", salah);
