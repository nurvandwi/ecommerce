<template>
  <div class="home">
    <HeaderShayna />
    <HeroShayna />
    <WomanShayna />
    <InstaShayna />
    <PartnerShayna />
    <Footer />
  </div>
</template>

<script>
import Footer from "@/components/Footer.vue";
import PartnerShayna from "@/components/PartnerShayna.vue";
import InstaShayna from "@/components/InstaShayna.vue";
import WomanShayna from "@/components/WomanShayna.vue";
import HeaderShayna from "@/components/HeaderShayna.vue";
import HeroShayna from "@/components/HeroShayna.vue";
export default {
  name: "Home",
  components: {
    HeaderShayna,
    HeroShayna,
    WomanShayna,
    InstaShayna,
    PartnerShayna,
    Footer
  }
};
</script>
