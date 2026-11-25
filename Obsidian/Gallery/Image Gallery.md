<div class="gallery">
    {% for file in files %}
    {% if file.path.startsWith("Gallery/") and
file.extension in ["png", "jpg", "jpeg", "gif"] %}
    <div class="gallery-item">
        <img src="{{ file.path }}" alt="{{ file.name
}}" width="300" height="200">
    </div>
    {% endif %}
    {% endfor %}
</div>
