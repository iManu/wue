<template>
    <div class="">
        <h1>{{ page.H1 }}</h1>

        <menu-secondary></menu-secondary>
        {{routename}}

        <h2>{{ page.H2 }}</h2>

        <router-link :to="{ name: 'Home' }">Home</router-link>
        <Inside></Inside>
    </div>
</template>

<script>
    import gql from 'graphql-tag';
    import MenuSecondary from '@/components/ui/MenuSecondary';
    import Inside from '@/components/Inside';

    // GraphQL query
    const pageQuery = gql`
        query getPage($route: String!) {
            page(route: $route) {
                H1
                H2
            }
        }
    `;

    export default {
        name: 'pageN1',
        components: {
            MenuSecondary,
            Inside,
        },
        data() {
            return {
                page: {},
                routename: this.$route.name,
            };
        },
        watch: {
            $route() {
                this.routename = this.$route.name;
            },
        },
        // props: {
        //     routename: {
        //         default: this.$route.name,
        //     },
        // },
        apollo: {
            page: {
                query: pageQuery,
                variables() {
                    return {
                        route: this.routename,
                    };
                },
            },
        },
    };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
    @import '~styles/main';

    h1, h2 {
      font-weight: normal;
    }

    ul {
      list-style-type: none;
      padding: 0;
    }

    li {
      display: inline-block;
      margin: 0 10px;
    }

    a {
      color: $online-color;
    }
</style>
