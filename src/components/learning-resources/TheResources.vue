<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
        <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add Resources</base-button>
    </base-card>
    <!--Keep-alive to keep data in the form when we switch between stored-resources and add-resource-->
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
    
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';
export default {
    components:{
        StoredResources,
        AddResource
        },
    data() {
        return {
            selectedTab: 'stored-resources',
            storedResources: [
            {
            id: 'official-guide',
            title: 'Official Guide',
            description: 'The Official Vue.Js documentation.',
            link: 'https://vuejs.org/',
            },
            {
            id: 'google',
            title: 'Google',
            description: 'Learn to Google...',
            link: 'https://google.com/',
            }
        ],
        }
    },
    provide(){
        return{
            resources: this.storedResources,
            //inject addResource Method To AddResource.vue 
            addResource: this.addResource,
            deleteResource: this.removeResource
        };
    },
    methods: {
        setSelectedTab(tab){
            this.selectedTab = tab;
        },
        addResource(title, description, url){
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: url
            };
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        },
        removeResource(resid){
            //don't create new array without the deleted resource cause is not working DOM already rendered
            const resIndex = this.storedResources.findIndex(res => res.id === resid);
            this.storedResources.splice(resIndex,1);
        }
    },
    computed:{
        storedResButtonMode(){
            return this.selectedTab === 'stored-resources' ? null : 'flat'
        },
        addResButtonMode(){
            return this.selectedTab === 'add-resource' ? null : 'flat'
        }
    }
    
}
</script>

<style scoped>

</style>