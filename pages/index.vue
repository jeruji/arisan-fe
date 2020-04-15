<template>
  <div class="container">
    <div class="margin-top-40">
      <vueper-slides autoplay>
        <vueper-slide v-for="i in 5" :key="i" :title="i.toString()"></vueper-slide>
        <template v-slot:pause>
          <i class="icon pause_circle_outline"></i>
        </template>
      </vueper-slides>
    </div>
    <div class="margin-top-40">
      <img src="../assets/dompet-bersama-bg.png" class="img-fluid" />
    </div>
    <div class="row margin-top-40">
      <div class="col-sm-4"><a href="#" class=""><img src="http://placehold.it/800X200" class="img-fluid"></a>
      </div>
      <div class="col-sm-8">
        <h3 class="title">How to Fight Fraud with Artificial Intelligence and Intelligent Analytics</h3>
        <p class="text-muted"><span class="glyphicon glyphicon-lock"></span> Available Exclusively for Premium Members</p>
        <p>Could artificial intelligence have been used to prevent the high-profile Target breach? The concept is not so far-fetched. Organizations such as Mastercard and RBS WorldPay have long relied on artificial intelligence to detect fraudulent transaction patterns and prevent card.</p>
        
        <p class="text-muted">Presented by <a href="#">Ellen Richey</a></p>
        
      </div>
    </div>
    <hr>
      <div class="row">
        <div class="col-sm-4"><a href="#" class=""><img src="http://placehold.it/800X200" class="img-fluid"></a>
        </div>
        <div class="col-sm-8">
          <h3 class="title">Big Payment Data: Leveraging Transactional Data to Ensure an Enterprise Approach to Risk Management</h3>
          <p class="text-muted"><span class="glyphicon glyphicon-calendar"></span> July 23, 2014 @ 1:30 PM</p>
          <p>60% of organizations were exposed to actual or attempted fraud loss last year. As fraud and risk increases year over year, the amount of data being collected increases as well.
            </p><p class="text-muted">Presented by <a href="#">Mike Braatz</a>, <a href="#">Jonathan Eber</a></p>
          
        </div>
      </div>
      <hr>
      <nav aria-label="Page navigation example">
      <ul class="pagination">
        <li class="page-item"><a class="page-link" href="#">«</a></li>
        <li class="page-item active"><a class="page-link" href="#">1</a></li>
        <li class="page-item"><a class="page-link" href="#">2</a></li>
        <li class="page-item"><a class="page-link" href="#">3</a></li>
        <li class="page-item"><a class="page-link" href="#">4</a></li>
        <li class="page-item"><a class="page-link" href="#">5</a></li>
        <li class="page-item"><a class="page-link" href="#">»</a></li>
      </ul>
      </nav>
  </div>
</template>

<script>
import { VueperSlides, VueperSlide } from 'vueperslides'
import 'vueperslides/dist/vueperslides.css'

export default {
  data() {
    return {
      slides: [
        {
          title: 'Slide #1',
          content: 'Slide content.'
        }
      ]
    }
  },
  components: {
    VueperSlides, VueperSlide
  }
}
</script>

<style>
.vueperslide {
  background: linear-gradient(-45deg, #EE7752, #E73C7E, #23A6D5, #23D5AB);
}
.vueperslide__title{
  font-size: 7em;
  opacity: 0.6;
}
.margin-top-40 {
  margin-top: 40px;
}
@media screen and (max-width: 768px) {
  .vueperslide__title {
    font-size: 2em;
  }
  .vueperslides__parallax-wrapper {
    padding-bottom: 50% !important;
  }
  .vueperslides__arrow svg {
    width: 3em;
  }
}
</style>
