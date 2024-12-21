<template>
    <div class="modal fade" id="randomJokeModal" tabindex="-1" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Random Joke</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <p>{{ joke }}</p>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
export default {
    props: ['joke'],
};
</script>
  