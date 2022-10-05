{% assign semanas = cursada | sort %}
{% for semana_hash in semanas reversed %}
{% assign numero_semana = semana_hash[0] | plus:0 %}
{% assign semana = semana_hash[1] %}

## [Semana {{numero_semana}}](#semana-{{numero_semana}}){: .titulo-semana}
{{semana.descripcion}}

{% if semana.videos %}
### Videos
Dejamos aquí algunos videos de cursadas anteriores que sirven para repasar y también subiremos las grabaciones de las clases virtuales
{% for video in semana.videos %}
{% if video.url %}
* [{{video.nombre}}]({{video.url}}). 
{% else %}
* {{video.nombre}} - en breve. 
{% endif %}
{% endfor %}
{% endif %}

{% if semana.conferencia %}
### Conferencia
{% if semana.conferencia.url %}
**Link**: [entrar acá]({{semana.conferencia.url}})
{% endif %}

{% if semana.conferencia.horarios %}
**Horarios**: {{semana.conferencia.horarios}}
{% endif %}

{% if semana.conferencia.horario0 %}
**Comisión Noche**: {{semana.conferencia.horario0}}
{% endif %}

{% if semana.conferencia.url0 %}
**Link Noche**: [entrar acá]({{semana.conferencia.url0}})
{% endif %}

{% if semana.conferencia.horario1 %}
**Comisión Mañana**: {{semana.conferencia.horario1}}
{% endif %}

{% if semana.conferencia.url1 %}
**Link Mañana**: [entrar acá]({{semana.conferencia.url1}})
{% endif %}

{% if semana.conferencia.horario2 %}
{{semana.conferencia.horario2}}
{% endif %}

{% endif %}

{% if semana.entrega %}

### Para entregar
{% assign fecha = semana.entrega.fecha %}
La fecha límite para la entrega de esta semana es el <strong>{% include fecha-formato-humano.md fecha=fecha %}</strong>.

{% assign guias = semana.entrega.mumuki %}
{% if guias %}
**Mumuki**
{% include ejercicios-mumuki.md guias=guias %}
{% endif %}

{% assign ejercicios = semana.entrega.ejercicios %}
{% if ejercicios %}
{% include ejercicios-github.html ejercicios=ejercicios %}
{% endif %}



{{semana.entrega.descripcion}}

{% endif %}

{% if semana.ejercicios %}

### Ejercicios para trabajar en clase
{% assign ejercicios = semana.ejercicios %}
{% include ejercicios-github.html ejercicios=ejercicios %}

{% if semana.textoEjercicios %}
{{semana.textoEjercicios}}
{% endif %}

{% endif %}

{% if semana.mumuki %}

### Ejercicios de Mumuki

Te recomendamos resolver las guías:
{% assign guias = semana.mumuki %}
{% include ejercicios-mumuki.md guias=guias %}

{% endif %}

{% if forloop.last == false %}
<hr class="titulo-semana">
{% endif %}

{% endfor %}
