---
title: "Documenting: Familiarizing Block Based Themes"
date: "2022-08-23"
categories: 
  - "documenting"
  - "work-notes"
category-slug: "work-notes"

---

**New Day:** Mon 21 Aug 2022 12:00:00 PM CDT

This article is a partner article to this [article](https://montelogic.com/?p=349). I would like to use BBT and FSE to replace the plugins I am using.

[talk](https://m.youtube.com/watch?v=S-6c-TrTC6Y&list=PL6dZTR-Ez9JCJuSLUEcMDPb7M9NrKCfZ7&index=1) on how to develop BBT:

Templates are HTML files that contain a full page of layout. They follow the same hierarchy of a typical WordPress theme that we are familiar with. Block template files are where you are are HTML files as well but they're meant to be reusable. Across multiple full-page templates.

I wonder what selecting code view in the block editor looks like.

The site editor has a panel that allows you to browse create templates and template parts.

if you have the Gutenberg plug installed. You can press the export button and that'll apparently export the changes that you made with. That wasn't made with code. This is very interesting.

Really, what I'm looking at is .... you could edit a site to match a large divi theme just based on the editor, export it and it would like like you did those same edits with php or css.

Block based themes use a lot of logic located in the theme json file making the use of style.css lower--thank god.

But you would still use the style.css file for custom block styles or for specific theme styles which would not be editable such as animations or transitions.

I'm watching the [video](https://www.youtube.com/watch?v=S-6c-TrTC6Y&list=PL6dZTR-Ez9JCJuSLUEcMDPb7M9NrKCfZ7&index=1&t=722s&ab_channel=WordPressNYC) WordPress NYC published discussing block based themes, in it a slide says "Wait, if users can customize the whole site. What's the purpose of a theme?"

Looking at how this FSE system works, I would answer with, essentially not really, it appears to be more of a jumping off point.

Note, I think that once the BBT paradigm really gets some steam behind it, I think that it will take a lot of jobs from the industry. More specifically, jobs--or gigs--in the WordPress ecosystem that require low amounts of skill.

I plan on reading the official documentation, [here](https://developer.wordpress.org/block-editor/).

I have noticed that you can't use widgets on BBT I wonder what the workaround to that is.

I am now watching this [video](https://www.youtube.com/watch?v=tsCT-18Udpw&list=PL6dZTR-Ez9JCJuSLUEcMDPb7M9NrKCfZ7&index=4&ab_channel=WPDevelopmentCourses), covering all the types of theme.

A block theme and a classic theme are so fundamentally different, it is very hard to create a bridge between the two.

Placing style rules within the theme.json makes things LOOK SO MUCH NEATER!

Looking at this, if a developer wanted to get really good at the logic behind these BBT and FSE systems, what you could do is ... offer your services to various plugin manufacturers as a service of updating their plugins to use FSE.

**Logged out:** Mon 22 Aug 2022 00:00:00 AM CDT

**New Day:** Mon 22 Aug 2022 04:36:10 PM CDT

I am going to work on an empty theme today and try my best to do that I can with the bare basics.

Question: What is the bare basics of a BBT theme?

I would think it would be the only theme.json file in the root folder and one template file folder.

Side Note: Gutenberg starts off in full screen mode and you are unable to view the post, exit full screen mode and the view post button will return. Use Ctrl+Shift+Alt+F to toggle this.

I will be following this [course](https://fullsiteediting.com/courses/full-site-editing-for-theme-developers/) along the way.

I have written a gist ([here](https://gist.github.com/MonteLogic/169a93ebaedfc58eeb3413725588cff7)) which will, "when executed scaffolds a theme structure with just the bare essentials of a BBT (Block Based Theme)".

Okay, now I am contrasting the bare-theme with the Ona theme.

Viewing the editor drawer of FSE pictured [here](https://lh3.googleusercontent.com/zLbdYBuf3Ui9k8MkJZx_N52LtgMzUB3AyOnAriXX155WhIsmhCBXcJkF1O2CHSOXuv_-e__Ta4nvXUTj1BtKNhd1uVpLaNZwj6Kri7MxQnyJyz5_9pj2Ipj7ubNoWi7OXaCBbQyRcovwEfe7Br2t1K2Y942iXMygsv39fJ71KLROaQeigzbB3zjye9_dlzoRkQYiC9KxgvfCIvWH2PmxoDwinrnp5bWPU4dHXipfMI8nV8Q4A5u5hBunx8BzHctNRlvUIMB3FJDQHeAFsHRd3d0axx7w3u81_w7m8tcenkF97ImXW-Pxz6M6PlxVS1Rr-8la1aStduqmVt1JiGxUG2RqV0jkdyW39ot31BP0yCQf2kQOARKiAfedtiZ_-vzWCPV3SMb0e1nmBP_HROpyoKhuComBK6FPFAtwy0DnLr_eg33GmROrFtQ45MI_bmlGfbe1nZmjiFoIRWc_IBgwiWNgUHpeJeiEiqIxfpnwXAPYiGw9QgV6HtognybBQ-Ke0lxfL462F7qJoTrI2T5ONWaAh0uCiqshHYnxZbrKRh3muvDopXumOwGMyd8qCQKPCvnaiokmnB_fYRSvAN-TRN5W4NtN1BBkPSks2eg21G6ZP9Ohfm4PUZJ8i-VpS2AyobJcna7ZscATglNjevLtMQOg2pFR705ccX9vfWNQhXctHSY0e8FQNtDtcxJkOpCv0bCV9y9LpPqNyaqOeWvJIjP-KFFohKGxsGtyvVswtq16HOtaqxqPd_M5TL6Fj3l5zJnkbGrLzK0RZqJvpHVGrdWTW5lRx-eJcJpz5SlScEJPsAB2kC_4ookEs1kPpjC_ScJZ=w238-h437-no?authuser=1).

This is what the Templates area of bare-bbt looks like ([here](https://lh3.googleusercontent.com/w3tUXjw0SkCmCOY7PE5JS1jqzDwJt-7SzN7mCPD2uRHYZjoop0UkaxS4uoAAOIB_reBoOxyrjDZHGxYr1XnPs7qAx_sKuAR6ogf0ZAGJ3i85VfK0jXbGurQ3He-mVfJFRmSgV971swfnh_bNwpz3DwNHM6eJB3nnYGgRgRvULXfWa31SlvIFxPyhsFUGSA1y1mrsEe9v7nu_XgdB7jD9Tf4G2AxEZY6qTXphld_A1mc6PIbgzSCWBpwtbATR9hCQiNX8HuAlWAQSv7SDesQBuDEFzzRMxxfL21D7pSj5necqDf_ofNeBOVAcNVEgfzyi0eQnoZHPC_zN31Rj2rQwDbG26Ud0Ftj-TuZ-W5JFu0dgYFHCUs8i8qyYjLgAzDPFqk5uO7guU6xwglhQy1l3IKhpmozh1Es8RlHpeYvPcJ_7UiHl3t68abCCecwKaN_ehb428Uqt28G5pN3P3O0qRBoKDk01McD-JhKjF_YJSSoCPKCCYvHOYGxuC6J4BIjhkbbhgxuursZGrF00t-jTRm8c9dYO0YuLETmz4XcUiUazvUWhwNQAgHwhs6yhls51qv__n0BbH-kwEUbuC1vUw-cpKkmBabjDZ5_07wuaLOI5idUB6abqTVvsHC3ecYdTQXq_V8Z8hkUXCkt5lhczcSiq5k04roM248zMf8D7JFhwaif1TIk58yi-Bjzl_rPG7FXNd0pugrotjl9tyPBT6QYnlabbl2SjNQ6dZUC77TmNtX8eeHga8Gmuwds-LMgee0GlzBrbElQEybpr-qjczUaKo8N5ysYUmLtnTHPYbQOKv1IhP1Zuc1Db4d6f4QfD_G-R=w382-h665-no?authuser=1)).

This is what the Template Parts area of bare-bbt looks like ([here](https://lh3.googleusercontent.com/71ZLntuNAMp8IOLf6tbEhtdMBi_U_HBimR-ajZIbRbHvulUsBvJ7gi__3vQ5X98_eo_4bhpmFcYn5EV9vtpwzHKwB76i-JZeAbXZubdippNwsqpi_2Ujv9Ff4vntJlxGCTRrSxzu8AbRAeb8kTu8cpeOzFWtl8cQh7seDR8kppEuEww1Yyrele_tsDjCdds9GLbJBgBzPiRDXLKMqYPmu1BrPaXyDY4Ou5ip6Ft-8C8NjoRaU-bmx10WIb38ab4tI66mDbT7yiNO3qugk4vTU5iBJkJVOnsjbFU9cBhAg6BWJ_-SnVuNzlqpCA55O8_3DyFsU1TZ8pYe9xFuJqFmmlV9SjSdI9T2xFZYZzqzbXJaNLo9BtHB2ziLt3RV8qqvO19hwt5YNKpEClg2H2yDkWTd3ypTna_XA487Kzz2DVsljX4oE4RBOCt6R4TCk8iVhwjkatiwzaFjtOvO4C36SlEf_-y0rp-CLfy3L7VyEMGJv-roBcLrBY9WlzO_B11ilAwD7sneyhndDbvtDh_RLeeM4ih9Ul1croWjha8bOzfo8iZIPNp26e1_AYoombNjILGb4DLneUCvZHzQHuEdjPMgKP9D5niWPK-lxgnc7oryKwqqnZBiovAg0miWHbWqq9-Yo6ml7toAK9PAC715YPyAm73yaVndxXwj4Jy9zcTwU5swCNyZoas9GwGg8fbW-YFRoMfPJKYlGDGUIYOzS1NV0NaXj1QWSBIaGcymNyUEqT9DUSBe-BaRsPvq80Wcr_0vhQ_5EW72X5WJjlQs84lY5CNeRrZ4EUsqUWF94rWv1UgAfFigJLMU9UXbif_YPRVf=w1920-h876-no?authuser=1)).

Okay, now that I know this, I would like to isolate and import the [Ona](https://wordpress.org/themes/ona/) menu from the test site with sample data.

Okay, looking at it I see nothing in Templates or Template Parts that say menu, so I'm thinking the menu logic is in the header.

Okay, I duplicated it and yeah the menu is in the header.

Alright, after making that custom menu, export that zip and then you can access your custom template.

Okay, I got that into a file named menu.html as a template part now let's add it to the bare theme.

I only added the Template Part and no styles. But somehow, the menu appears to be functioning well. Experiencing this process ..... I am blown away.. NO cap.

Before the theming that I was doing if I had to make a custom theme, getting the menu to link and the JavaScript as well it was like a 45 minute job linking all of the code together so the menu JavaScript would run well. This is incredible. It just worked right away... what.

What's even more remarkable is that it's responsive and when it is in mobile mode the menu looks fine.

[Mobile menu](https://lh3.googleusercontent.com/7YgvzEZ-C5XHdEZF2VBx5hE3j4ZxO6EikEDmpuyet76JmvdS6PVAggGlzKODOHyXp-z3Jvf5Kcqxg_7GfoM3KIQUr13oUzFqHBIRlknDttOGwMdoVxY0mbPX0xE2TWKjw8XvEgtq1IJCDPE0IolJe_YyUJaEwr0aqa9G0rKwcNepwiXWY4NNawqITBJm2R890ulXDmyrMC4Bza-ZqYTrncx2DnJnBhrBNNedyQuCBQoBw_CH_d5pURLIHqyigsCaRysJpwCL8Nv-DaoJBEWYI1d58IlWiZnkeaU5dj2QCmDZ69j76Lt-smV4DP3PsFndHDXvZA75wW6idTs2-5pCu23KwkXNoKOB1_1VhST96VHMj1kNJSZH1OPWy4asKi8rQuz8MuzJSsIShhaAzR6s5zxGKusKESTKG06DicqVb5bXzitd-GsiLgqnxtyECJooG1AEqXAEHkA_8A661TOS7JNILNI5-IudMMm5UD6wFXB2zP714RuuaSvMjB3QWDDyZx0-_GtxF1gi4jhjx7lbAxAz5G--AdgfyI81R_tJeV9V2f0pyYPEzciF5N8PGiJazLuFjQi63ej5C1h18eeLtrQH53dN6w8ooCDD8d8UmHb_pePqr1IWeXWV7NCldJacpScsxJ6RB-iqR6q6h_bKd5N0kGKBGjfyxMdPgI5vv8aXp0THuVPYLVyQX6iboNPY5XVI7zIeG0RaXzsfEjbC1JkmNvfFJaX6KAahLSlI9QDc695Dcf5TLnS33bRbFroxD_z35-9uOe8fgQ7-UGjiEb2s4I4uP1Kzvb3LC6DeVWBARuEAJaOo2UdYggiwMg_RiS4b=w494-h254-no?authuser=1) and [Mobile menu expanded](https://lh3.googleusercontent.com/vkyU2SXrUVgnay9kEmrryfBlmnVZcIdxq-Mni9_sUDYVmg2ZUC_b5BSXWVHd7mQzxT-mfp0kp1rzTDoz2fwxO8qTGa-j43PUw379gZnjrEaZmrShFiDqL-paeD4GvqX8Jr1I7yW1iHTl0DG2x4hjwEvRxcQtJ7pbufg2Pm1FgF3vNSjbhO4r9mSRV8uBurSsp0V7FLPCDat9EmWfK1_-jSBWr-54XiEgTkGmbO-kkhp-DX0c52v16utQ9-crI_lPlKcNBMAgzAQeDLiPoNspjmVZ3hF6i9Y7q2PuRoR6lXFvu3oraNAIA9azG-woQr17r-mIAL-olCDb7NpAx3XPTYHT6xWAJDThfS8dHRS--vTAeh_vYk3du4AfsjkEv3nb3DNR75pF4JS9TVJXMD3q_WXUPJKQsas0oQq6XBgIfgDRUp6W8B09unQsXDRuh3t2T4FhFFxJmfegt6a6DjcNLMmtW-_qlpSbivsFA10juISy3MUScOGVWrMF1wVIa0A4UBE-bXTuVjOBN6XryhcebKhX6uAE8mjlM_eMjAXBdfEoMLVFT4lYOopv1tlQ3APZQabWU3rfcmPy1DJNcXWDGTY1mDYohWSZpW964nc71jmlbILrNsdh07KtFqs27Wqg-DqSJb_OBgLf0ClZv1-Y8a_AjBpdKQrHgcPWyS4o7ExDlIEnMnV_bJ4cyJSXU4r65DCVUUiHG-2_GOQgI9ze1Sdhb5OE8943qfG1RHRvjGG0ri8Eyvz0EhmbVAUuvJ014AotO47F8pP6JIANJlAxC4JI1XXMzBp9AvPjbqYT0G9qkSwWa-swa-wUQFahtw4odyIp=w450-h816-no?authuser=1)

[Desktop menu](https://lh3.googleusercontent.com/79G24C_yxk6JXVUYolwYQQJFMnLgyWLDpC5veVP5wNOdkV7l_jbGekVUHYB64A61qAEttQnwmjQBzilT_R5irHl5lOfj0-LVc0TTn1OM-YYdVf2ee1rcMSRmbTGWe75XKfFltJD-LvMmQ-d6giFhy-JDeQCTdV0508eNAU-VMHnzvp8u7uCLS5yjks7BcKXjQMnul-NLK0sPZp_WCD5CN1F4neBrZSs9baNm778FNNiPCqRsCOyC6Ux39XC42TzqgwMGYUkjOPY9eJ1KgDGo_5FgUJmqihR3pTots9I7EL5KXi68fCvwEpxR9nkBh3tfcW3LZb2fUFpp-XZ29UvYTIJeCb18ZQDPnLo4yPnT-T-PiAMDjSYpWsQhGMzN4HgCGvj53gVqKieDXTgzPzxNWk7VYVnbdMujrI-r1rsJk2qNreBEXk_wUVOgfgQ68p0lVipaC1aHZDz3fpzppq4a1P4aZOCvgPYGrQk-ovQ5dtWE3iD4f38ms0i-4We0IRr3TzbXLRbWZQq0LU-tY6DzwA1VAredO9Bi9ACPuM8EiWl7DG1hPMjnHQhnXeGUa1MOQN3dVSrS0vIA-ce5oo8mL0dbJyF9OCc9uYhsEOvbtIXov3i5e44eD37PxyEvPqEHxMa7jBQjFAxTEwMWUhIbroLDhHY0bHyFl_P61NPA7Kz_piZIJ2t38OlTb0H9U4guPT3IF8hX-Wslg7QyE2k1OQ1VPUxuugiahiSXG85ue_9JrLMYu6Ky25BOJvTaY4Ht-oBfnU3arZ9yFzIScVgcUiz0DovSxdAF5wQh_93Dvczgf-1FUmR3s-Qo9Ai6e33B4F-B=w959-h438-no?authuser=1)

I don't know where the styles are for this or how it's doing it but I look forward to this research.

With that being said...

**Logging out:** Tue 23 Aug 2022 02:46:06 AM CDT

**New Day:** Wed 24 Aug 2022 10:50:07 PM CDT

Use / then type the name of the desired block you want and it'll pop up. This only works if your on a new block and / is the first character that you type.
