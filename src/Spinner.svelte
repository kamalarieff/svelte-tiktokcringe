<div class="flex relative justify-center items-center h-[175px]">
    <div class="ring-of-dots"/>
</div>

<style>
     :root {
         --loading-half-color: #919191;
         --loading-full-color: #5e5e5e;
     }

     /**
     * Ring of dots
     *
     * @author jh3y
   */
     @-webkit-keyframes ring-of-dots {
     0% {
       -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color);
               box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color); }
     14.28571% {
       -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 var(--loading-half-color), -4.45042px -19.49856px 0 0 var(--loading-full-color), 12.4698px -15.63663px 0 0 white;
               box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 var(--loading-half-color), -4.45042px -19.49856px 0 0 var(--loading-full-color), 12.4698px -15.63663px 0 0 white; }
     28.57143% {
       -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 var(--loading-half-color), -18.01938px -8.67767px 0 0 var(--loading-full-color), -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
               box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 var(--loading-half-color), -18.01938px -8.67767px 0 0 var(--loading-full-color), -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
     42.85714% {
       -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 var(--loading-half-color), -18.01938px 8.67767px 0 0 var(--loading-full-color), -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
               box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 var(--loading-half-color), -18.01938px 8.67767px 0 0 var(--loading-full-color), -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
     57.14286% {
       -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 var(--loading-half-color), -4.45042px 19.49856px 0 0 var(--loading-full-color), -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
               box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 var(--loading-half-color), -4.45042px 19.49856px 0 0 var(--loading-full-color), -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
     71.42857% {
       -webkit-box-shadow: 20px 0px 0 0 var(--loading-half-color), 12.4698px 15.63663px 0 0 var(--loading-full-color), -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
               box-shadow: 20px 0px 0 0 var(--loading-half-color), 12.4698px 15.63663px 0 0 var(--loading-full-color), -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
     85.71429% {
       -webkit-box-shadow: 20px 0px 0 0 var(--loading-full-color), 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 var(--loading-half-color);
               box-shadow: 20px 0px 0 0 var(--loading-full-color), 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 var(--loading-half-color); }
     100% {
       -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color);
               box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color); } }
   @keyframes ring-of-dots {
     0% {
       -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color);
               box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color); }
     14.28571% {
       -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 var(--loading-half-color), -4.45042px -19.49856px 0 0 var(--loading-full-color), 12.4698px -15.63663px 0 0 white;
               box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 var(--loading-half-color), -4.45042px -19.49856px 0 0 var(--loading-full-color), 12.4698px -15.63663px 0 0 white; }
     28.57143% {
       -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 var(--loading-half-color), -18.01938px -8.67767px 0 0 var(--loading-full-color), -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
               box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 var(--loading-half-color), -18.01938px -8.67767px 0 0 var(--loading-full-color), -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
     42.85714% {
       -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 var(--loading-half-color), -18.01938px 8.67767px 0 0 var(--loading-full-color), -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
               box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 var(--loading-half-color), -18.01938px 8.67767px 0 0 var(--loading-full-color), -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
     57.14286% {
       -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 var(--loading-half-color), -4.45042px 19.49856px 0 0 var(--loading-full-color), -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
               box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 var(--loading-half-color), -4.45042px 19.49856px 0 0 var(--loading-full-color), -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
     71.42857% {
       -webkit-box-shadow: 20px 0px 0 0 var(--loading-half-color), 12.4698px 15.63663px 0 0 var(--loading-full-color), -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
               box-shadow: 20px 0px 0 0 var(--loading-half-color), 12.4698px 15.63663px 0 0 var(--loading-full-color), -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
     85.71429% {
       -webkit-box-shadow: 20px 0px 0 0 var(--loading-full-color), 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 var(--loading-half-color);
               box-shadow: 20px 0px 0 0 var(--loading-full-color), 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 var(--loading-half-color); }
     100% {
       -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color);
               box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color); } }

   .ring-of-dots:before {
     animation: ring-of-dots 1s infinite linear reverse;
     border-radius: 10px;
     content: '';
     display: block;
     height: 10px;
     width: 10px;
   }
</style>
