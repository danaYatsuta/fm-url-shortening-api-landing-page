<script>
import LinkListForm from './LinkListForm.vue'
import LinkListItem from './LinkListItem.vue'

let id = 0

export default {
  components: {
    LinkListForm,
    LinkListItem
  },
  data() {
    return {
      links: []
    }
  },
  methods: {
    addLink(newLink) {
      newLink.id = id++
      this.links.push(newLink)

      sessionStorage.setItem('saved_links', JSON.stringify(this.links))
    }
  },
  created() {
    const savedLinks = JSON.parse(sessionStorage.getItem('saved_links'))

    if (savedLinks) {
      this.links = savedLinks
      id = this.links.length
    }
  }
}
</script>

<template>
  <div>
    <LinkListForm @addLink="(newLink) => addLink(newLink)" />

    <div class="mt-6 flex flex-col gap-6 md:gap-4">
      <LinkListItem
        v-for="link in links"
        :key="link.id"
        :url="link.url"
        :shortenedUrl="link.shortenedUrl"
      />
    </div>
  </div>
</template>
