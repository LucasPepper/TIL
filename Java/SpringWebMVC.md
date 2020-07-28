# Spring Web MVC

Este módulo do Spring utiliza o padrão da arquitetura MVC para administrar o projeto. São utilizados vários conceitos de @Annotations, onde o Spring identifica certos padrões passados pelo desenvolvedor, aplicando metodologias pré-programadas.

Sabe-se que o Spring também administra/injeta dependências no projeto, por isso é importante adicioná-las ao começar o projeto.

Segue um exemplo arbitrário que utiliza annotations, juntamente com métodos HTTP:

```java
@Controller
public class JediController {

    // Identificação e Injeção de dependência: repository
    @Autowired
    private JediRepository repository;

    // Mapeamento do método HTTP GET
    @GetMapping("/jedi")
    public ModelAndView jedi() {

        final ModelAndView modelAndView = new ModelAndView();
        modelAndView.setViewName("jedi");

        final Jedi luke = new Jedi("Luke", "Skywalker");
        modelAndView.addObject("allJedi", repository.getAllJedi());
        return modelAndView;
    }

    @GetMapping("/new-jedi")
    public ModelAndView newJedi() {

        final ModelAndView modelAndView = new ModelAndView();
        modelAndView.setViewName("new-jedi");

        modelAndView.addObject("jedi", new Jedi());
        return modelAndView;
    }

    // Converter os dados passados por Post para um objeto Jedi
    @PostMapping("/jedi")
    public String createJedi(@Validated @ModelAttribute Jedi jedi, BindingResult result, RedirectAttributes redirectAttributes) {

        if (result.hasErrors()) {
            return "new-jedi";
        }

        repository.add(jedi);

        // Message: no html, o Thymeleaf já adicionou um campo "${message}" (text)
        redirectAttributes.addFlashAttribute("message", "Jedi cadastrado com sucesso!");

        // Redirecionar a um caminho especificado
        return "redirect:jedi";
    }
}
```
9