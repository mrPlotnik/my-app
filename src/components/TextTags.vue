<template>
<v-container class="tags__container">    

    <v-row :class="['tags__row', alignmentClass]">
        <div 
            v-for="el in visibleItems"
            :key="el.id"
            :class="['tags__item', {'d-none': !el.show}]"
        >       
            <v-chip
                v-if="el.type === 'tag'"
                :ref="el.id"
                class="tags__tag"                
            >
                <v-icon v-if="el.data.icon" left>{{ el.data.icon }}</v-icon>
                {{ el.data.text }}
            </v-chip>
            <v-icon v-else :ref="el.id">
                mdi-circle-small
            </v-icon>            
        </div>
    </v-row>

    <!-- Скрытый -->
    <v-row :class="['tags__row fan', alignmentClass]">
        <div 
            v-for="el in combinedItems"
            :key="el.id"
            class="tags__item"
        >       
            <v-chip
                v-if="el.type === 'tag'"
                :ref="el.id"
                class="tags__tag"                
            >
                <v-icon v-if="el.data.icon" left>{{ el.data.icon }}</v-icon>
                {{ el.data.text }}
            </v-chip>
            <v-icon v-else :ref="el.id">
                mdi-circle-small
            </v-icon>            
        </div>
    </v-row>

</v-container>
</template>

<script>
export default {
    name: 'TextTags',

    props: {
        tags: { type: Array, required: true },
        alignment: { 
            type: String,
            default: 'left',
            validator: value => ['left', 'justify'].includes(value)
        }
    },

    data() {
        return {
            visibleItems: [],
        };
    },

    mounted() {
        this.visibleItems = this.combinedItems;  
        this.calculateVisibleTags();
        window.addEventListener('resize', this.calculateVisibleTags);
    },
    beforeDestroy() {
        window.removeEventListener('resize', this.calculateVisibleTags);
    },

    computed: {
        alignmentClass() {
            return this.alignment === 'justify' ? 'tags--justify' : 'tags--left';
        },
        combinedItems() {
            const combinedItems = [];
            let uniqueId = 0;

            this.tags.forEach((tag, index) => {
                combinedItems.push({ type: 'tag', data: tag, id: `tag-${uniqueId++}`, show: true });
                if (index < this.tags.length - 1) {
                    combinedItems.push({ type: 'separator', id: `separator-${uniqueId++}`, show: true });
                }
            });
            return combinedItems;
        },        
    },

    methods: {          
        calculateVisibleTags() {
            const parent = this.$el;    
            const parentRect = parent.getBoundingClientRect();
            
            
            for (let i = 0; i < this.combinedItems.length; i++) {
                const itemEl = this.$refs[this.combinedItems[i].id][0].$el;
                const itemRect = itemEl.getBoundingClientRect();

                const isCompletelyVisible = itemRect.left >= parentRect.left && itemRect.right <= parentRect.right   

                if (isCompletelyVisible) {
                    itemEl.classList.remove('hidden');                    
                    this.visibleItems[i].show = true;
                } else {
                    if (i % 2 === 0) {
                        this.visibleItems[i].show = false;
                        this.visibleItems[i - 1].show = false;
                    }                    
                }            
            }
        }
    }
};
</script>

<style scoped lang="scss">
.tags {
    &__container {
        position: relative;
    }
    &__row {
        flex-wrap: nowrap;
        overflow: hidden;
        padding: 1em;
        border-radius: .75em;
        background-color: #f1f1f1;
        &.fan {
            position: absolute;
            top: 0;
            margin: 0;
            visibility: hidden;
            z-index: -1;
        }
    }
    &__item {
        display: flex;
    }
    &__tag {
        white-space: nowrap;
    }
    &--left {
      justify-content: flex-start;
    }
    
    &--justify {
      justify-content: space-between;
    }
}
</style>
