<script>
const featureToggleApi = require('feature-toggle-api');

const api = new featureToggleApi();

function vuePlugin(api)
{
    Object.assign(api,{
    props: {
      name: {
        type: String
      },
      variant: {
        type: String
      },
      data: {
        type: [Object, String]
      },
      tag: { 
        type:String,
        default:'div'
      }
    },
    name : 'feature',
    data () {
      return {
        isVisible: api.isVisible(this.name,this.variant,this.data)
      }
    },
    render: function (createElement) {
      if (this.isVisible) {
        return createElement(this.tag, {
          'feature-name': this.name,
          'feature-variant': this.variant
        }, this.$slots.default)
      }
    },
    methods: {
      _isVisible: function(name,variant,data){
        return api.isVisible(name,variant,data);
      }
    }
  })
}

api.addPlugin(vuePlugin);
module.exports = api;
</script>
 
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>