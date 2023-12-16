csharp
// Создаем C# скрипт для перемещения персонажа по поверхности

using UnityEngine;

public class CharacterMovement : MonoBehaviour
{
    // Объявляем переменную скорости и делаем ее сериализуемой
    [SerializeField] private float speed = 3f;
    private SpriteRenderer sprite;

    private void Start()
    {
        // Получаем компонент SpriteRenderer у дочернего объекта
        sprite = GetComponentInChildren<SpriteRenderer>();
    }

    private void Update()
    {
        // Если кнопка горизонтального ввода нажата, выполняем функцию перемещения
        if (Input.GetButton("Horizontal"))
        {
            Run();
        }
    }

    private void Run()
    {
        // Получаем значение для направления от правой оси
        Vector3 dir = transform.right * Input.GetAxis("Horizontal");

        // Перемещаем персонажа в направлении dir со скоростью speed
        transform.position = Vector3.MoveTowards(transform.position, transform.position + dir, speed * Time.deltaTime);

        // Отображаем персонажа в зеркальном отражении, если он движется влево
        sprite.flipX = dir.x < 0.0f;
    }
}
