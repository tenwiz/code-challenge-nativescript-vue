<template>
    <Page>
        <FlexboxLayout class="page">
            <StackLayout class="form">
                <Label class="font-32" textWrap="true" :text="getFullName" />
            </StackLayout>
            <StackLayout class="form">
                <Image :src="img" />
            </StackLayout>
        </FlexboxLayout>
    </Page>
</template>

<script>
export default {
    props: ['user', 'img'],
    computed: {
        getFullName: function() {
            return 'Thank you, ' + this.user.firstname + ' ' + this.user.lastname + '!';
        }
    },
}
</script>

<style scoped>

.font-32 {
    display: flex;
    color: #fff;
    font-size: 32;
    text-align: center;
}

.page {
    align-items: center;
    flex-direction: column;
    background: linear-gradient(to bottom, #1e5799 0%,#7db9e8 100%);
}

.form {
    margin-left: 30;
    margin-right: 30;
    flex-grow: 2;
    vertical-align: middle;
}
</style>
