<template>
    <footer id="footer">
      <div id="developer-info">
        <div class="links-stack">
          <a class="site-link link" href="" target="_blank">GitHub
            repo & utveckling</a>
          <a class="site-link link"
            href=""
            target="_blank">Databas och API</a>
        </div>
        <div class="links-stack border-style">
          <a class="site-link link" href=""
            target="_blank">Dataset-dokumentation</a>
          <div class="download-section">
            <a href="#" class="download-link link" @click="">Ladda ner data</a>
            <!-- <img v-if="isLoading" :src="Spinner" class="spinner" alt="Laddar..." /> -->
          </div>
        </div>
        <div class="links-stack border-style extra">
          <a class="site-link link" href="" target="_blank">Feedback</a>
        </div>
      </div>
      <div class="partners">
        <a href="https://dh.gu.se/">
          <div class="link GRIDHLogo" id="">GU / GRIDH</div>
        </a>
  
        <a href="">
          <div class="link PartnerLogo" id="">SweTerror</div>
        </a>
  
  
      </div>
    </footer>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  
  const isLoading = ref(false);
  
/*   const downloadData = async () => {
    isLoading.value = true;
    let url = 'https://saintsophia.dh.gu.se/api/inscriptions/inscription/?depth=2';
    const allData = [];
  
    try {
      while (url) {
        const response = await fetch(url);
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
  
        const pageData = await response.json();
        allData.push(...pageData.results);
  
        url = pageData.next ? pageData.next.replace(/^http:/, 'https:') : null;
      }
  
      triggerDownload(allData, 'inscriptionData.json');
    } catch (error) {
      console.error('Error fetching data:', error);
    } finally {
      isLoading.value = false;
    }
  };
  
  const triggerDownload = (data: any[], filename: string) => {
    const jsonBlob = new Blob([JSON.stringify(data)], { type: 'application/json' });
    const downloadUrl = window.URL.createObjectURL(jsonBlob);
    const link = document.createElement('a');
    link.href = downloadUrl;
    link.download = filename;
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
    window.URL.revokeObjectURL(downloadUrl);
  }; */
  </script>
  
  <style>
  .download-section a {
    display: inline;
  }
  
  .download-section {
    display: inline-flex;
    align-items: center;
  }
  
  
  #footer {
    display: block;
    background-color: #222;
    color: white;
    line-height: 1;
    height: 82px;
    width: calc(100% + 2px);
    font-size: 12px;
    position: absolute;
    z-index: 3000;
    bottom: -2px;
    font-family: "Barlow Condensed", sans-serif;
  }
  
  a {
    font-weight: bold;
  }
  
  .partners {
    float: right;
    position: fixed;
    bottom: 0px;
    right: 0px;
    height: 80px;
    width: 600px;
  }
  
  .GRIDHLogo {
    float: right;
    margin-top: 30px;
    width: auto;
    height: auto;
    text-align: left;
    font-weight: 100;
    font-style: normal;
    font-size: 30px;
    line-height: 0.8;
    padding: 0px 40px 5px 30px;
    vertical-align: middle;
  }
  
  
  .PartnerLogo {
    float: right;
    margin-top: 30px;
    width: auto;
    height: auto;
    text-align: left;
    font-weight: 100;
    font-style: normal;
    font-size: 30px;
    line-height: 0.8;
    padding: 0px 30px 5px 30px;
    vertical-align: middle;
    border-width: 0px 0.5px 0px 0px;
    border-color: white;
    border-style: solid;
  }
  
  #developer-info {
    display: flex;
    align-items: flex-end;
    margin-left: 35px;
    margin-top: 15px;
    font-size: 1.5em;
    line-height: 1.4;
    font-weight: 200;
  }
  
  .border-style {
    border-width: 0 0 0 0.5px;
    border-color: white;
    border-style: dashed;
    padding-left: 20px;
    padding-right: 10px;
  }
  
  .link {
    color: white;
  }
  
  .link:visited {
    color: white;
  }
  
  .link:hover {
    opacity: 0.8;
  }
  
  .download-link {
    background: url("https://data.dh.gu.se/ui-icons/download_white_circle.png");
    background-size: 18px;
    background-position: 0px 50%;
    background-repeat: no-repeat;
    padding-left: 25px;
    margin-left: 0px;
  }
  
  .site-link {
    background: url("https://data.dh.gu.se/ui-icons/arrow_link_white_circle.png");
    background-size: 18px;
    background-position: 0px 50%;
    background-repeat: no-repeat;
    padding-left: 25px;
  
  }
  
  .links-stack {
    margin-right: 20px;
  }
  
  .links-stack a {
    display: block;
  }
  
  #developer-info a:link {
    font-weight: 200;
  }
  
  @media screen and (max-width: 1090px) {
    .partners {
      display: none;
    }
  }
  
  @media screen and (max-width: 1210px) {
    .extra {
      display: none;
    }
  }
  </style>