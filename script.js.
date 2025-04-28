let draggedItem = null;
let offsetX = 0;
let offsetY = 0;
let isDragging = false;
let currentLevel = 1;

document.addEventListener('DOMContentLoaded', () => {
    const draggables = document.querySelectorAll('.draggable');
    const dropzones = document.querySelectorAll('.dropzone');

    draggables.forEach(item => {
        item.addEventListener('mousedown', dragStart);
        item.addEventListener('touchstart', dragStart);
    });

    document.addEventListener('mousemove', dragging);
    document.addEventListener('touchmove', dragging);

    document.addEventListener('mouseup', dragEnd);
    document.addEventListener('touchend', dragEnd);

    dropzones.forEach(zone => {
        zone.addEventListener('mouseup', dropItem);
        zone.addEventListener('touchend', dropItem);
    });
});

function dragStart(e) {
    e.preventDefault();
    isDragging = true;
    draggedItem = e.target;
    if (e.type === "touchstart") {
        offsetX = e.touches[0].clientX - draggedItem.getBoundingClientRect().left;
        offsetY = e.touches[0].clientY - draggedItem.getBoundingClientRect().top;
    } else {
        offsetX = e.offsetX;
        offsetY = e.offsetY;
    }
}

function dragging(e) {
    if (!isDragging || !draggedItem) return;
    let x, y;
    if (e.type === "touchmove") {
        x = e.touches[0].clientX;
        y = e.touches[0].clientY;
    } else {
        x = e.clientX;
        y = e.clientY;
    }
    draggedItem.style.position = 'absolute';
    draggedItem.style.left = (x - offsetX) + 'px';
    draggedItem.style.top = (y - offsetY) + 'px';
}

function dragEnd() {
    isDragging = false;
}

function dropItem(e) {
    if (!draggedItem) return;
    const dropzone = e.target.closest('.dropzone');
    if (dropzone) {
        dropzone.appendChild(draggedItem);
        draggedItem.classList.add('sorted');
        checkLevelCompletion();
    }
}

function checkLevelCompletion() {
    const unsorted = document.querySelectorAll('.draggable:not(.sorted)');
    if (unsorted.length === 0) {
        if (currentLevel === 1) {
            setTimeout(() => {
                nextLevel();
            }, 500);
        } else {
            alert('You finished the game!');
        }
    }
}

function nextLevel() {
    currentLevel = 2;
    document.getElementById('level1').style.display = 'none';
    document.getElementById('level2').style.display = 'block';
}
