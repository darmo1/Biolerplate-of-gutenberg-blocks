# Boilerplate-of-gutenberg-blocks

if(!defined('ABSPATH')) exit;

/* Resgister Gutenberg Block and CSS */
add_action('init', 'menneskeneRegisterBlock');
function menneskeneRegisterBlock(){

 /* If gutenberg don't exist so return nothing  */
    if(!function_exists('register_block_type')){
        return;
    }
    
    //Register every gutenberg Block
    
    wp_register_script(
        'gb-editor-script',
         plugins_url('build/index.js', __FILE__), 
         array('wp-blocks', 'wp-i18n', 'wp-element','wp-editor'), 
         filemtime( plugin_dir_path(__FILE__). 'build/index.js')
        );

    //Style to Editor

    wp_register_style(
        'gb-editor-styles',
        plugins_url('build/editor.css', __FILE__), 
        array('wp-edit-blocks'), 
        filemtime( plugin_dir_path(__FILE__). 'build/editor.css')
    );

    //Style to Frontend
    wp_register_style(
        'gb-frontend-styles',
        plugins_url('build/style.css', __FILE__), 
        array(), 
        filemtime( plugin_dir_path(__FILE__). 'build/style.css')
    );

	// array of blocks
    $blocks = array(
		'pg/menneskene',
    );

    foreach($blocks as $block){
        register_block_type($block, array(
            'editor_script' => 'gb-editor-script',
			'editor_style' => 'gb-editor-styles',
            'style' => 'gb-frontend-styles'
        ));
    }

}
