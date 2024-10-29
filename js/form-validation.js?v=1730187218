function formValidation($form) {
    var methodName = $form.prop('method').toLowerCase();
    if (methodName !== 'post') {
        return false;
    }
    var errors = [ ];
    var $inputs = $form.find('input[required=required]');
    if ($inputs.length > 0) {
        $inputs.each(function() {
            var noError = true;
            var type = $(this).attr('type');
            var value = $(this).val();
            console.log(value, type);
            switch (type) {
                case 'text':
                    noError = validateText(value);
                    break;
                case 'email':
                    noError = validateEmail(value);
                    break;
                case 'tel':
                    noError = validateTel(value);
                    break;
                case 'number':
                    noError = validateNumber(value);
                    break;
            }
            errors.push(noError);
            var postfix = $(this).attr('id');
            var $errorElement = $('#err-'+postfix);
            if (type === 'email') {
                if (validateText(value)) {
                    $('#err-email').hide();
                    $errorElement = $('#err-emailvld');
                }
            }

            if (noError === false) {
                $errorElement.show();
            } else {
                if (type === 'email') {
                    $errorElement = $('[id^=err-email]');
                }
                $errorElement.hide();
            }
        })
    }

    return errors.indexOf(false) === -1;
}

function validateText(text) {
    return $.trim(text) !== '';
}

function validateEmail(email) {
    var re = /^(([^<>()[\]\.,;:\s@\"]+(\.[^<>()[\]\.,;:\s@\"]+)*)|(\".+\"))@(([^<>()[\]\.,;:\s@\"]+\.)+[^<>()[\]\.,;:\s@\"]{2,})$/i;
    return re.test(email);
}

function validateTel(tel) {
    var re = /^[\+]?[0-9]{1,3}?[-\s\.]?[(]?[0-9]{1,5}[)]?[-\s\.]?[0-9]{1,3}[-\s\.]?[0-9]{1,6}[-\s\.]?[0-9]{1,6}$/im;
    return re.test(tel);
}

function validateNumber(number) {
    var re = /\d/g;
    return re.test(number);
}

function onGetInTouchSubmit() {
    alert('on get in touch');
    var $form = $('form[name="get-in-touch"]');
    if (!formValidation($form)) {
        e.preventDefault();
        return;
    }
}

$('body').on('submit', 'form[name="subscribe"]', function(e) {
    var $form = $('#subscribe');
    if (!formValidation($form)) {
        e.preventDefault();
        return;
    }
});

$('body').on('submit', 'form[name="get-in-touch"]', function(event) {
    if (!grecaptcha.getResponse()) {
        event.preventDefault(); //prevent form submit
        grecaptcha.execute();
    }
    onGetInTouchSubmit();
});

$('body').on('submit', 'form[name="ajax-form"]', function(e) {
    var $form = $('#subscribe');
    if (!formValidation($form)) {
        e.preventDefault();
        return;
    }
});


grecaptcha.ready(function() {
    // do request for recaptcha token
    // response is promise with passed token
    grecaptcha.execute('6Lf__bgiAAAAADSx-iuWHigwnZPC_gZEOTOvvkd4', {action:'validate_captcha'})
        .then(function(token) {
            // add token value to form
            var inputs = $('input.g-recaptcha-response');
            inputs.each((ind, elem) => $(elem).val(token));
        });
});