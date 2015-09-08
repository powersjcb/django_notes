# Rails to Django

## Analogous concepts
### 1. urls.py -> routes.rb

### 2. serializer.py -> rails strong params

Use serializer to handle

``` cats_controller.rb
def cat_params
   require(:cat).permit(:id, :cat_name)
end
```

```cats/serializers.py
from rest_framework import serializers
from .models import Cat

def CatSerializer(serializers.Serializer):

)
```
